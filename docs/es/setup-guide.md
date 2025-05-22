---
hide:
  - navigation
---

# **Guía de configuración**

## 🔧 **Instrucciones de instalación**

### ⚙️ Backend

Para el uso de nuestra aplicación, es fundamental tener instalados en nuestro sistema Python 3 o versiones superiores, así como también Pip, un gestor de paquetes y librerías para Python. Para cumplir esto, bastaría con ejecutar:

``` sh
apt-get install python3 python3-pip
```

También es necesario el paquete `Just`, un paquete de software que permite correr comandos complejos en formas acortadas llamadas "recetas" para así hacer uso de aquellas creadas por el docente que faciliten y agilicen la instalación de nuestra aplicación. Para ello, instalamos con:

``` sh
apt-get install rust-just # (1)
```

1. Puede ser, en vez de `rust-just`, simplemente `just`. Probar eso en caso de errores.

Y una vez tenemos instalados dicho paquete, podemos instalar la aplicación y sus dependencias con los siguientes pasos:

- Creamos el entorno virtual
``` sh
python -m venv .venv --prompt jukabox
```

- Activamos el entorno virtual
``` sh
source .venv/bin/activate
```

- Instalamos las dependencias
``` sh
pip install -r requirements.txt
```

Una vez instaladas las dependencias en un entorno virtual activado, realizamos las migraciones con:

``` sh
just check
just makemigrations
just migrate
```

Cuando todo lo anterior esté hecho, podemos iniciar nuestra aplicación con:

```sh
just 
```

### 🎨 Frontend

Es necesario instalar el gestor de paquetes de Node.js, npm, para manejar las dependencias de la aplicación. Esto se puede hacer ejecutando el siguiente comando:

```sh
sudo apt install npm
```

El siguiente comando lee el archivo package.json y descarga todos los módulos necesarios para la ejecución de la aplicación:

```sh
npm install
```

Una vez completado lo anterior, ejecutamos el siguiente comando para iniciar la aplicación:

```sh
npm run dev
```


## 📋 **Requisitos**

### 📡 Backend

**Dependencias generales**

* **asgiref==3.8.1**
  Soporte para **ASGI**, el estándar para servidores web asincrónicos en Python (usado por Django para manejar WebSockets, tareas async, etc.).
* **certifi==2025.1.31**
  Proporciona un conjunto actualizado de certificados raíz de confianza (HTTPS). Lo usa `requests`.
* **charset-normalizer==3.4.1**
  Detecta y normaliza codificaciones de texto. Lo usa `requests`.
* **click==8.1.8**
  Librería para crear interfaces de línea de comandos. Útil en herramientas como `Flask` o scripts personalizados.
* **idna==3.10**
  Soporta dominios internacionales (con caracteres Unicode) en URLs. Usado por `requests`.
* **sqlparse==0.5.3**
  Analizador de SQL. Django lo usa para formatear consultas SQL legibles en la terminal.
* **urllib3==2.4.0**
  Cliente HTTP de bajo nivel, usado por `requests` para hacer peticiones web.


**Framework principal**

* **Django==5.1.5**
  Framework web principal usado para construir el backend. Incluye ORM, vistas, rutas, autenticación, etc.


**Complementos Django**

* **django-colorfield==0.11.0**
  Campo personalizado para modelos de Django que permite seleccionar colores en el admin (por ejemplo, `ColorField` con selector de color).
* **django-cors-headers==4.6.0**
  Permite controlar y habilitar **CORS** (Cross-Origin Resource Sharing), útil para APIs accesibles desde frontends en otros dominios (como React o Vue).
* **django-rq==3.0.1**
  Integra **RQ** (Redis Queue) con Django para ejecutar tareas en segundo plano (como envío de emails o procesamiento de imágenes).


**Tareas en segundo plano**

* **rq==2.3.2**
  Librería principal de **Redis Queue**, usada para ejecutar tareas asíncronas con un sistema de colas basado en Redis.
* **redis==5.2.1**
  Cliente Python para conectarse a servidores **Redis**, usado por `rq`, `django-rq` y otras tareas que necesitan almacenamiento rápido en memoria.


**Multimedia**

* **pillow==11.1.0**
  Biblioteca para manejar imágenes en Python. Django la usa para campos de imagen (`ImageField`), redimensionar, convertir, etc.


**APIs externas**

* **musicbrainzngs==0.7.1**
  Cliente para la API de **MusicBrainz**, útil si tu app necesita buscar información sobre artistas, álbumes o canciones.


**Herramientas adicionales**

* **rust-just==1.38.0**
  Utilidad para automatizar comandos y tareas como si fuera un "Makefile", pero más moderno. Útil para scripts en desarrollo o despliegue.


### 🖼️ Frontend

**Herramientas básicas**

* **vue** `^3.5.13`
  El **núcleo del framework Vue.js** (versión 3). Sirve para construir componentes y apps reactivas del lado del cliente.
* **vue-router** `^4.5.0`
  Sistema de **ruteo** oficial de Vue 3. Permite navegación entre páginas/vistas sin recargar la web (SPA).
* **pinia** `^2.3.0`
  Sistema de **estado global** para Vue 3. Reemplazo moderno de Vuex: más ligero, con mejor integración en Composition API.


**Internacionalización**

* **vue-i18n** `^10.0.5`
  Plugin para **traducir tu aplicación** Vue a múltiples idiomas.
* **i18n** `^0.15.1`
  Una librería más general para internacionalización. A menudo no es necesaria si ya usas `vue-i18n`. Puede ser un residuo del proyecto o usada para otras tareas.


**Estilo y componentes**

* **bootstrap** `^5.3.3`
  Framework CSS para **estilizar componentes rápidamente** (botones, formularios, rejillas, etc.).
* **bootstrap-icons** `^1.11.3`
  Conjunto de **iconos SVG** que combinan con Bootstrap.


**Comunicación con el backend**

* **axios** `^1.7.9`
  Cliente HTTP para hacer **peticiones AJAX/REST** (GET, POST, etc.) desde el frontend a una API.


**Notificaciones**

* **vue-toast-notification** `^3.1.3`
  Muestra **notificaciones tipo "toast"** (mensajes emergentes y breves) al usuario, útiles para confirmar acciones, errores, etc.