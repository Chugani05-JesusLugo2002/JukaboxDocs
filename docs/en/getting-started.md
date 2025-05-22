---
hide:
  - navigation
---

# 🚀 **Getting started**

## 🔧 **Installation instructions**

### ⚙️ Backend

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

### 🎨 Frontend

You need to install Node.js's package manager, npm, to manage the application's dependencies. This can be done by running the following command:

```sh
sudo apt install npm
```

The following command reads the `package.json` file and downloads all the modules required to run the application:

```sh
npm install
```

Once the above is completed, run the following command to start the application:

```sh
npm run dev
```

## 📋 **Requirements**

### 📡 Backend

**General Dependencies**

* **asgiref==3.8.1**
  Support for **ASGI**, the standard for asynchronous web servers in Python (used by Django to handle WebSockets, async tasks, etc.).
* **certifi==2025.1.31**
  Provides an up-to-date set of trusted root certificates (HTTPS). Used by `requests`.
* **charset-normalizer==3.4.1**
  Detects and normalizes text encodings. Used by `requests`.
* **click==8.1.8**
  Library for creating command-line interfaces. Useful in tools like `Flask` or custom scripts.
* **idna==3.10**
  Supports international domains (with Unicode characters) in URLs. Used by `requests`.
* **sqlparse==0.5.3**
  SQL parser. Django uses it to format readable SQL queries in the terminal.
* **urllib3==2.4.0**
  Low-level HTTP client, used by `requests` to make web requests.

**Main Framework**

* **Django==5.1.5**
  Main web framework used to build the backend. Includes ORM, views, routing, authentication, etc.

**Django Add-ons**

* **django-colorfield==0.11.0**
  Custom field for Django models that allows selecting colors in the admin (e.g., `ColorField` with a color picker).
* **django-cors-headers==4.6.0**
  Allows controlling and enabling **CORS** (Cross-Origin Resource Sharing), useful for APIs accessible from frontends on other domains (like React or Vue).
* **django-rq==3.0.1**
  Integrates **RQ** (Redis Queue) with Django to run background tasks (like sending emails or processing images).

**Background Tasks**

* **rq==2.3.2**
  Main library of **Redis Queue**, used to run asynchronous tasks with a Redis-based queue system.
* **redis==5.2.1**
  Python client for connecting to **Redis** servers, used by `rq`, `django-rq`, and other tasks that require fast in-memory storage.

**Multimedia**

* **pillow==11.1.0**
  Library for handling images in Python. Django uses it for image fields (`ImageField`), resizing, converting, etc.

**External APIs**

* **musicbrainzngs==0.7.1**
  Client for the **MusicBrainz API**, useful if your app needs to search for information about artists, albums, or songs.

**Additional Tools**

* **rust-just==1.38.0**
  Utility for automating commands and tasks like a "Makefile", but more modern. Useful for development or deployment scripts.

### 🖼️ Frontend

**Basic Tools**

* **vue** `^3.5.13`
  The **core of the Vue.js framework** (version 3). Used to build reactive client-side components and apps.
* **vue-router** `^4.5.0`
  Official **routing system** for Vue 3. Allows navigation between pages/views without reloading the page (SPA).
* **pinia** `^2.3.0`
  **Global state management** system for Vue 3. A modern replacement for Vuex: lighter, with better integration in the Composition API.

**Internationalization**

* **vue-i18n** `^10.0.5`
  Plugin to **translate your Vue application** into multiple languages.
* **i18n** `^0.15.1`
  A more general internationalization library. Often not needed if you're already using `vue-i18n`. May be a project leftover or used for other tasks.

**Styling and Components**

* **bootstrap** `^5.3.3`
  CSS framework for **quickly styling components** (buttons, forms, grids, etc.).
* **bootstrap-icons** `^1.11.3`
  Set of **SVG icons** that pair well with Bootstrap.

**Communication with the Backend**

* **axios** `^1.7.9`
  HTTP client for making **AJAX/REST requests** (GET, POST, etc.) from the frontend to an API.

**Notifications**

* **vue-toast-notification** `^3.1.3`
  Displays **"toast"-style notifications** (short, popup messages) to the user, useful for confirming actions, showing errors, etc.
