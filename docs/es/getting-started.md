---
hide:
  - navigation
---

# 🚀 **Primeros pasos**

## 🔐 **Autenticación de usuarios**

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

## 🗂️ **Modelo de datos**

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

## 🧱 **Estructura del código**

### 🛠️ Backend

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

### 🎨 Frontend

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


## 💻 **Tecnologías y Herramientas**

**Entornos de desarrollo y herramientas:**  

- **Visual Studio Code** como editor principal con extensiones como Django, Prettier, Error Lens y snippets personalizados que nos facilitaron el trabajo otorgándonos eficiencia.  
- **Git** para el control de versiones.  
- **SQLite** como sistema de gestión de bases de datos, utilizado por defecto por el framework de Django.

**Lenguajes:**
Se utilizaron **Python**, **SQL** y **TypeScript** como lenguajes de programación. Para la estructura y el diseño de la interfaz web, se emplearon **HTML**, **CSS** y **SCSS** como lenguajes de marcado y estilo.

**Frameworks:**
Los principales frameworks fueron **Django** para el desarrollo del backend, **Vue.js** para el frontend, y **Bootstrap** para el diseño responsivo y estético de la interfaz.

**Librerías:**
Entre las librerías destacadas se encuentran:

* **django-rq**, para la ejecución de tareas en segundo plano (como el procesamiento de imágenes o envío de correos electrónicos).
* **vue-toast-notifications**, para mostrar notificaciones emergentes al usuario.
* **vue-i18n**, que facilita la internacionalización de la aplicación.
* **Pinia**, como sistema de gestión de estado global en Vue.

**Tecnologías complementarias:**
Se utilizó **Redis** como sistema de cola para la ejecución eficiente de tareas asincrónicas a través de django-rq.

### El Importer como tarea desacoplada


## 🎨 **Decisiones de diseño**

### ⚙️ Justificación de Tecnologías

- **Django:** Elegido por ser un framework robusto y escalable que facilita el desarrollo rápido de aplicaciones web seguras gracias a su arquitectura basada en el patrón MTV (Modelo-Template-Vista) y su enfoque en DRY (Don’t Repeat Yourself).
- **Pillow:** Permite manipular imágenes de manera eficiente, lo cual es fundamental para funcionalidades como redimensionamiento, conversión de formatos, o generación de imágenes dinámicas.
- **IPython:** Herramienta interactiva ideal para depuración y pruebas rápidas de funciones Python durante el desarrollo.
- **django-rq:** Gestiona tareas en segundo plano mediante Redis Queue, lo cual permite mejorar la eficiencia del sistema al delegar operaciones costosas como el procesamiento de imágenes o el envío masivo de correos electrónicos.
- **Vue.js:** Elegido por ser un framework progresivo, ligero y flexible que permite construir interfaces de usuario reactivas mediante una arquitectura basada en componentes. Facilita el desarrollo modular y escalable de aplicaciones web.
- **Pinia:** Seleccionado como sistema de gestión de estado oficial de Vue.js por su simplicidad, integración nativa con Composition API y compatibilidad con TypeScript. Mejora la organización del estado global y su trazabilidad durante el desarrollo.
- **vue-toast-notifications:** Utilizado para mostrar notificaciones emergentes de manera clara y no intrusiva, permitiendo una retroalimentación inmediata al usuario sobre acciones realizadas, como operaciones exitosas o errores.
- **ESLint:** Implementado como herramienta de análisis de código para garantizar buenas prácticas de programación, detectar errores potenciales y mantener un estilo de código limpio y coherente en todo el proyecto.
- **Bootstrap:** Incorporado como framework de diseño CSS para agilizar la creación de interfaces responsivas y estéticamente consistentes, reduciendo tiempos de desarrollo gracias a su sistema de grillas y componentes reutilizables.
- **vue-i18n:** Adoptado para la internacionalización de la aplicación, permitiendo la adaptación del contenido a múltiples idiomas de forma sencilla y dinámica, y mejorando así la accesibilidad a usuarios de distintos contextos lingüísticos.

### 🧩 Justificación de Enfoques y Patrones

- **Arquitectura basada en componentes:** Modularizar la aplicación en componentes reutilizables y en apps independientes dentro de Django favorece la escalabilidad, mantenibilidad y facilita el trabajo colaborativo al aislar funcionalidades específicas.
- **Modularidad mediante apps:** Dividir el proyecto en apps independientes permite un desarrollo más organizado y escalable, facilitando el mantenimiento y la colaboración.
- **Gestión de tareas en segundo plano:** El uso de django-rq permite delegar procesos intensivos (como procesamiento de imágenes o envíos de correos masivos) fuera del flujo principal, mejorando la eficiencia y experiencia del usuario.
- **Optimización y manejo eficiente de recursos:** Utilización de Pillow para el procesamiento y compresión de imágenes, reduciendo carga en el frontend y mejorando el rendimiento.
- **Arquitectura basada en componentes:** Vue.js estructura la interfaz en componentes reutilizables y encapsulados que facilitan la escalabilidad y mantenibilidad de la aplicación.
- **Gestión de estado centralizada con Pinia:** Permite controlar el estado global de la aplicación de forma predecible y reactiva, mejorando la organización del código y facilitando la depuración.
- **Internacionalización con vue-i18n:** Implementa un patrón para separar los textos del código lógico, facilitando la traducción y soporte multilingüe sin afectar la estructura.
- **Notificaciones emergentes con vue-toast-notifications:** Mejora la experiencia del usuario mediante feedback inmediato y no intrusivo ante acciones importantes.
- **Diseño responsive con Bootstrap:** Asegura que la interfaz se adapte correctamente a distintos dispositivos, garantizando accesibilidad y usabilidad.