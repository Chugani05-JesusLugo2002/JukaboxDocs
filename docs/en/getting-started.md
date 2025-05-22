---
hide:
  - navigation
---

# 🚀 **Getting started**

## **Data Model**

## **Code Structure**


## 💻 **Technologies and Tools**

**Languages:**
**Python**, **SQL**, and **TypeScript** were used as programming languages. For the structure and design of the web interface, **HTML**, **CSS**, and **SCSS** were used as markup and style languages.

**Frameworks:**
The main frameworks used were **Django** for backend development, **Vue.js** for the frontend, and **Bootstrap** for responsive and aesthetic interface design.

**Libraries:**
Notable libraries include:

* **django-rq**, for executing background tasks (such as image processing or email sending).
* **vue-toast-notifications**, to display popup notifications to users.
* **vue-i18n**, which facilitates the internationalization of the application.
* **Pinia**, as the global state management system in Vue.

**Complementary Technologies:**
**Redis** was used as a queue system to efficiently execute asynchronous tasks via django-rq.

**Development Environments and Tools:**

* **Visual Studio Code** as the main editor, with extensions such as Django, Prettier, Error Lens, and custom snippets that improved efficiency.
* **Git** for version control.
* **SQLite** as the database management system, used by default by the Django framework.


## 🎨 **Design Decisions**

### ⚙️ Technology Justification

* **Django:** Chosen for being a robust and scalable framework that facilitates rapid development of secure web applications thanks to its architecture based on the MTV pattern (Model-Template-View) and its DRY (Don’t Repeat Yourself) philosophy.
* **Pillow:** Allows efficient image manipulation, essential for features like resizing, format conversion, or dynamic image generation.
* **IPython:** An interactive tool ideal for debugging and quick testing of Python functions during development.
* **django-rq:** Manages background tasks using Redis Queue, improving system efficiency by offloading costly operations like image processing or bulk email sending.
* **Vue.js:** Chosen for being a progressive, lightweight, and flexible framework that enables building reactive user interfaces with a component-based architecture. It facilitates modular and scalable web development.
* **Pinia:** Selected as Vue.js's official state management system for its simplicity, native integration with the Composition API, and TypeScript compatibility. It improves global state organization and traceability during development.
* **vue-toast-notifications:** Used to display clear, non-intrusive toast notifications, providing immediate feedback to users for actions like successful operations or errors.
* **ESLint:** Implemented as a code analysis tool to enforce good coding practices, detect potential issues, and maintain a clean, consistent code style throughout the project.
* **Bootstrap:** Included as a CSS design framework to streamline the creation of responsive and visually consistent interfaces, reducing development time with its grid system and reusable components.
* **vue-i18n:** Adopted for application internationalization, enabling dynamic and straightforward content adaptation to multiple languages, improving accessibility for users from different linguistic backgrounds.

### 🧩 Approach and Pattern Justification

* **Component-based architecture:** Modularizing the application into reusable components and independent Django apps enhances scalability, maintainability, and team collaboration by isolating specific functionalities.
* **Modularity through apps:** Dividing the project into independent apps allows for more organized and scalable development, simplifying maintenance and collaboration.
* **Background task management:** Using django-rq offloads intensive processes (like image processing or mass emailing) from the main execution flow, improving system efficiency and user experience.
* **Resource optimization and efficient handling:** Use of Pillow for image processing and compression reduces frontend load and improves performance.
* **Component-based architecture:** Vue.js structures the interface into reusable and encapsulated components that support application scalability and maintainability.
* **Centralized state management with Pinia:** Enables predictable and reactive control of global state, improving code organization and simplifying debugging.
* **Internationalization with vue-i18n:** Implements a pattern to separate texts from logic, facilitating translation and multilingual support without affecting structure.
* **Popup notifications with vue-toast-notifications:** Enhances user experience by providing immediate and non-intrusive feedback for key actions.
* **Responsive design with Bootstrap:** Ensures the interface adapts properly to various devices, guaranteeing accessibility and usability.
