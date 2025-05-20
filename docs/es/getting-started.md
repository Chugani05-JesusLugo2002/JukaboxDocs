---
hide:
  - navigation
---

# **Primeros pasos**

## **Instrucciones de instalación**

### Backend

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

### Frontend

## **Requirements**