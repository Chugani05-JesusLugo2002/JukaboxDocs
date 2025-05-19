---
hide:
  - navigation
---

# Maintanance

## **Política de mantenimiento**

### Introducción

Esta política tiene como objetivo garantizar que nuestra plataforma reciba el mantenimiento adecuado para asegurar su funcionamiento óptimo, su seguridad y el cumplimiento de las expectativas de los usuarios. Esta política cubre tanto las actualizaciones regulares de software como el soporte técnico disponible para resolver incidencias.

### Frecuencia de Actualizaciones

Las actualizaciones son fundamentales para mantener la web actualizada, con nuevas funcionalidades, mejoras de seguridad y solución de errores. La frecuencia de las actualizaciones será la siguiente:

- **Actualizaciones de Seguridad:** Se realizarán de manera **inmediata** tan pronto como se detecten vulnerabilidades críticas o riesgos de seguridad. En caso de emergencias de seguridad, se ejecutarán parches de manera prioritaria.
- **Actualizaciones Menores:** Estas incluyen mejoras de rendimiento, optimización y solución de errores no críticos. Se realizarán de manera **mensual**, salvo que una actualización urgente sea necesaria debido a una falla importante.
- **Actualizaciones Mayores:** Estas pueden implicar cambios significativos en la funcionalidad o características del sistema. Se realizarán **trimestralmente** o según lo exijan las necesidades de la plataforma o cambios tecnológicos importantes.

### Soporte Técnico

El soporte técnico estará disponible para resolver cualquier inconveniente relacionado con la página web. La cobertura y los tiempos de respuesta son los siguientes:

- **Soporte 24/7:** Para fallos de alto impacto, el soporte estará disponible las 24 horas del día, los 7 días de la semana.
- **Soporte Regular:** Los problemas menos críticos, el soporte estará disponible de **lunes a viernes**, de 9:00 AM a 6:00 PM.
- **Tiempo de Respuesta:**
  - **Emergencias (Alta prioridad):** El tiempo de respuesta será de **máximo 2 horas**.
  - **Problemas de baja prioridad:** El tiempo de respuesta será de **máximo 24 horas**.
  - **Consultas o mejoras menores:** Se atenderán dentro de un plazo de **48 horas**.

### Proceso de Actualización

El proceso para realizar actualizaciones y mantenimiento será el siguiente:

  - **Planeación:** Las actualizaciones mayores serán notificadas con **mínimo 1 semana de antelación**.
  - **Pruebas:** Antes de implementar actualizaciones críticas o mayores, se realizarán pruebas en un entorno de desarrollo o staging para asegurar que no se afecten otras funcionalidades del sistema.
  - **Implementación:** Las actualizaciones se implementarán durante **ventanas de mantenimiento preestablecidas** que se comunicarán con antelación a los usuarios.
  - **Monitoreo post-actualización:** Después de la actualización, se realizará un monitoreo intensivo para detectar cualquier posible incidencia.

### Exclusiones

Esta política de mantenimiento no cubre:

  - **Actualizaciones por causas externas:** Las actualizaciones debidas a cambios en el entorno de terceros (por ejemplo, cambios en sistemas operativos, navegadores o plataformas externas) no están incluidas.
  - **Fallas no relacionadas con el mantenimiento del sistema:** El soporte técnico no cubrirá problemas que no sean derivados de un mal funcionamiento o actualización del sitio web gestionado.

### Mejoras Continuas

Nos comprometemos a una mejora continua en la calidad de nuestras actualizaciones y en la disponibilidad del soporte, para proporcionar la mejor experiencia a nuestros usuarios y garantizar la eficiencia de los sistemas implementados.

## **Registro de cambios (Changelog)**

### Versión 1.0.0 - 17 de diciembre de 2024

**Lanzamiento Inicial:**

- **Primera versión estable** de la plataforma disponible para los usuarios.
- Funcionalidad principal: Ofrecer una plataforma educativa integral que facilita el intercambio de contenidos académicos, gestión de calificaciones y emisión de certificados para instituciones educativas.
- Interfaz de usuario: Diseño simple e intuitivo para facilitar la navegación.
- Sistema de autenticación: Inclusión de inicio de sesión con usuario y contraseña.
- Base de datos inicial implementada con SQLite.

**Características incluidas:**

- Generación de informes en PDF.
- Soporte para múltiples idiomas, está en desarrollo.

**Mejoras:**

- Estabilidad y rendimiento optimizados para garantizar una experiencia de usuario fluida.

**Correcciones:**

- Se implementaron pruebas iniciales para garantizar la calidad y confiabilidad de la aplicación.

**Notas:**

- Se trata de la **primera versión estable** del producto. Continuaremos mejorando y añadiendo nuevas características en futuras actualizaciones.

### Notas

- Todos los cambios importantes se comunican a través de actualizaciones automáticas.
- Las actualizaciones menores, parches y correcciones de errores se incluyen en versiones de mantenimiento como la 1.0.1.


## **Plan de escalabilidad**

### Arquitectura Técnica
- **Despliegue Modular:** Dividir los componentes de la plataforma (gestión de lecciones, calificaciones, certificados, autenticación) en microservicios para facilitar el mantenimiento y escalabilidad.  
- **Balanceo de Carga:** Implementación de balanceadores de carga para distribuir el tráfico entre servidores.  

### Mantenimiento y Optimización
- **Integración Continua (CI/CD):** Configurar pipelines automáticos para pruebas, integración y despliegue utilizando herramientas como GitHub Actions.  
- **Auditorías Técnicas:** Revisiones periódicas para optimizar consultas, limpieza de código y mejoras de seguridad.  

### Mejora del Rendimiento
- **Optimización de Consultas:** Uso de ORM (como Django ORM) junto con optimización manual para consultas críticas.  

### Seguridad 
- **Gestión Segura de Usuarios:** Cifrado de contraseñas, autenticación multifactor (MFA), y políticas de roles/permiso.  
- **Protección de Datos:** Cumplimiento de normativas como el RGPD para la protección de datos de estudiantes y profesores.  

### Funcionalidades Futuras
- **Gamificación:** Incorporación de logros y recompensas para fomentar la participación de los estudiantes.  
- **Soporte Multilingüe:** Ampliación de la plataforma a múltiples idiomas.  

### Escalabilidad del Equipo Técnico
- **Documentación Clara:** Mantenimiento de manuales técnicos detallados para nuevos desarrolladores.  