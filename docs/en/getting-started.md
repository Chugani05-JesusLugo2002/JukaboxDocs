---
hide:
  - navigation
---

# **Getting started**

## **Installation instructions**

### Backend

To use our application, it's essential to have Python 3 or higher installed on your system, as well as Pip, a package and library manager for Python. To do this, simply run:

``` sh
apt-get install python3 python3-pip
```

You also need the `Just` package, a software package that allows you to run complex commands in shortened forms called "recipes". You can use those created by the teacher to make installing our application faster and easier. To do this, we install it with:

``` sh
apt-get install rust-just # (1)
```

1. Instead of `rust-just`, you could simply use `just`. Try that in case of errors.

And once we have installed this package, we can install the application and its dependencies with the following steps:

- We create the virtual environment
``` sh
python -m venv .venv --prompt jukabox
```

- We activate the virtual environment
``` sh
source .venv/bin/activate
```

- We install the dependencies
``` sh
pip install -r requirements.txt
```

Once the dependencies are installed in an activated virtual environment, we carry out the migrations with:

``` sh
just check
just makemigrations
just migrate
```

When all the above is done, we can start our application with:

```sh
just runserver
```

### Frontend

## **Requirements**