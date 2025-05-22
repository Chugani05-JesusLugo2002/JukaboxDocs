---
hide:
  - navigation
---

# **Guía de configuración**

## **Modelo de datos**


## **Estructura del código**

## 💻 **Tecnologías y Herramientas**

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

**Entornos de desarrollo y herramientas:**  

- **Visual Studio Code** como editor principal con extensiones como Django, Prettier, Error Lens y snippets personalizados que nos facilitaron el trabajo otorgándonos eficiencia.  
- **Git** para el control de versiones.  
- **SQLite** como sistema de gestión de bases de datos, utilizado por defecto por el framework de Django.


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