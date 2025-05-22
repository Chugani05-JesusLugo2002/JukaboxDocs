---
hide:
  - navigation
---

# **Guía de configuración**

## **Autenticación de usuarios**

En nuestra aplicación, la baja, alta y modificación de usuarios se gestiona mediante la interfaz administrativa de Django (siempre y cuando tengas las credenciales de administrador) y las distintas herramientas que proporciona, como por ejemplo, el comando de gestión `createsuperuser` que permite la creación de usuarios administradores en el sistema. Además, por necesidades al momento del desarrollo, hemos creado un pequeño comando de gestión propio llamado `createfakeusers` que permite la creación de uno o varios usuarios, con sus respectivos perfiles de la aplicación, asignando datos falsos, para la realización de pruebas futuras.

``` py
class Command(BaseCommand):
    help = 'Sign up profiles with given usernames.'

    def add_arguments(self, parser):
        parser.add_argument('usernames', nargs='+', help='List of usernames to create profiles for')
        
    def handle(self, *args, **kwargs):
        usernames = kwargs['usernames']
        for username in usernames:
            email = f"{username}@example.com"
            try:
                user = User.objects.create_user(username=username, email=email, password='1234')
                profile = Profile.objects.create(user=user) 
                self.stdout.write(self.style.SUCCESS(f'Successfully created profile for {username} with id {profile.id}'))
            except Exception as e:
                self.stdout.write(self.style.ERROR(f'Error creating profile for {username}: {e}'))
```

## **Modelo de datos**

La decisión de trabajar con la API de MusicBrainz y el aprendizaje sobre ellas nos ayudó a alcanzar un diseño final del modelo de datos: hemos adaptado tal diseño para que haga uso de la completa API de MusicBrainz sin complicaciones y lograr una automatización del trabajo, algo fundamental que se abarca más adelante en la documentación.

``` mermaid
erDiagram
  Artist }o--o{ Album : have
  Album }|--|{ Song : belongs
  User ||--|| Profile : have
  Profile }o--o{ Song : likes
  Profile }o--o{ Album : likes
  Profile }o--o{ Artist : likes
  Profile ||--o{ Review : write
  Song ||--o{ Review : have
```

La naturaleza de red social da mucho como explicación para la cantidad de relaciones que el modelo `Profile` tiene en el ecosistema de Jukabox.

## **Estructura del código**

### Backend

Por este lado en nuestra API, distintas *apps* han sido creadas para segmentar los diferentes modelos, vistas y serializadores que son usados en Jukabox:

1. **Accounts**: Dedicada al inicio de sesión, registro y cerrado de sesión de los usuarios así como también el comando de gestión `createfakeusers` ubicado en esta *app*.
2. **Albums**: Dedicada a la gestión de los álbumes.
3. **Artists**: Dedicada a la gestión de los artistas.
4. **Songs**: Dedicada a la gestión de las canciones y las *reviews*.
5. **Users**: Dedicada a la gestión de los perfiles y *likes*.
6. **Importer**: Dedicado a la importación de datos y enlaces externos.
7. **Shared**: Aspectos comunes de la aplicación, como el buscador del sitio web.

Parte de las *apps* comparten similitudes con su funcionamiento, pues aplicaciones como *Artists*, *Albums* o *Songs* contienen distintas vistas que devuelven resultados rápidos para mostrar en diferentes secciones del sitio web.

``` py
@check_method('GET')
def most_liked_songs(request: HttpRequest) -> JsonResponse:
    songs = Song.objects.all().order_by('-likes')[:6]
    serializer = SongSerializer(songs, request=request)
    return serializer.json_response()
```

Un ejemplo sería la vista anterior, que es la encargada de devolver las seis canciones con más "me gusta".

Luego tenemos otras vistas con un funcionamiento algo más complejo, como el siguiente:

```py
@check_method('POST')
@check_json_body
@assert_body_fields('artist_mbid')
@assert_token
def import_artist(request: HttpRequest) -> JsonResponse:
    mbid = request.data['artist_mbid']
    mbid_pattern = r'^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$'
    if not (m := re.fullmatch(mbid_pattern, mbid)):
        return JsonResponse({'error': 'Invalid MBID'}, status=400)
    import_artist_data.delay(mbid)
    if Artist.objects.get(mbid=mbid):
        return JsonResponse({'message': f'Updating artist data...'})
    return JsonResponse({'message': f'Adding artist data...'})
```

Esta es la vista principal del *Importer* en la que se puede apreciar el uso de diferentes decoradores (para un uso más eficiente de código), casa de texto con expresiones regulares y el control de errores mediante clausuras guardas.

### Frontend

El *frontend* tiene naturaleza de *Single Page Application*, fácilmente lograda con la tecnología que ofrece Vue como framework para ello, tanto por el uso de sus librerías `vue-router` o Pinia, como por la flexibilidad que ofrece sus *Single File Component* (SFC): ficheros en su formato especial que permite encapsular la lógica, el estilo y el esqueleto de los componentes o elementos web.

Por otro lado, la estructura que llevamos en el *frontend* está enfocada en el principio de *"Feature-based Organization"*, es decir, la organización y separación de los ficheros según la característica que trabaja, algo similar a la forma en la que se organizan las *apps* de *Django*. Teniendo esto en cuenta, los elementos que poseemos son:

1. **Components**: Los distintos elementos disponibles en nuestro sitio web, los cuales se clasifican según funcionalidad.
    - **Layout**: Secciones comunes del sitio web como el *Header* o *Footer*
    - **Elements**: Componentes utilizados en vistas u otros componentes específicos.
    - **Elements/shared**: Componentes comunes en el sitio web.
    - **Classes**: Interfaces de Typescript implementadas.
2. **Composables**: Estructuras de código reutilizable, en nuestro caso, `useAPI.ts` que contiene todas las funciones necesarias para realizar peticiones de datos a la API en Django, y `useSocial.ts`, que a pesar de ser similar, tiene un cierto enfoque en las acciones realizadas por el usuario como dar *likes* o enviar una *review*.
3. **Locales**: Ficheros de idioma.
4. **Router**: Donde encontramos el código que gestiona las urls y el sistema de navegación del sitio web.
5. **SCSS**: Ficheros SCSS con elementos comunes como colores, utilizados en el sitio web.
6. **Stores**: Donde se encuentran las *stores* de Pinia, en nuestro caso, `useAuthStore`, que gestiona la autenticación del usuario.
7. **Views**: Y finalmente, las vistas o *RouterView*, fundamentales para el funcionamiento del sitio web y su naturaleza como *Single Page Application* (SPA).

## **Tecnologías y Herramientas**

### El Importer como tarea desacoplada

## **Decisiones de diseño**

### Justificación de Tecnologías

### Justificación de Enfoques y Patrones