[⬅️ Volver](index.md#documentación-del-proyecto-mvc-enlaces)

---

# 📁 Estructura de Carpetas

La organización de las carpetas en un proyecto MVC es crucial para mantener un código limpio, modular y fácil de mantener. A continuación, se describe la estructura utilizada en el proyecto **MVC Enlaces de SOFTWARE**, con explicaciones de los directorios más importantes.

---

## 📂 Estructura General del Proyecto
---

El proyecto **MVC Enlaces de SOFTWARE** está organizado en varias carpetas principales que corresponden a los tres componentes del patrón MVC y otros elementos esenciales. A continuación, se describe cada sección.

??? info "Estructura Principal del Proyecto"
    === "Descripción"
        La estructura del proyecto está compuesta por las siguientes carpetas y archivos principales:
        
        - **`controllers/`**: Contiene las clases que manejan la lógica de la aplicación.
        - **`models/`**: Contiene la lógica relacionada con los datos, como consultas a la base de datos.
        - **`views/`**: Contiene los archivos que definen la interfaz del usuario.
        - **`public/`**: Contiene recursos públicos como archivos CSS, JavaScript e imágenes.
        - **`vendor/`**: Incluye las dependencias de terceros gestionadas por Composer.
        - **`index.php`**: Punto de entrada de la aplicación.
        - **`.env`**: Configuración del entorno para variables sensibles.

    === "Ejemplo de Estructura"
        ```plaintext
        c:/servidor/www/exame-final-it/
        ├── controllers/
        │   ├── Autoload.php
        │   ├── EnlacesController.php
        │   ├── FiltrarDatos.php
        │   ├── Router.php
        │   ├── SelectElement.php
        │   └── ViewController.php
        ├── models/
        │   └── Model_crud.php
        ├── views/
        │   ├── error401.php
        │   ├── error404.php
        │   ├── footer.php
        │   ├── header.php
        │   └── home.php
        ├── public/
        │   ├── css/
        │   │   ├── alerts.css
        │   │   ├── buttons_Confirmar.css
        │   │   ├── buttons_SmartGrid.css
        │   │   ├── cards.css
        │   │   ├── cards_SmartGrid.css
        │   │   ├── colors_backgrounds.css
        │   │   ├── select_filter.css
        │   │   ├── table_SmartGrid.css
        │   │   └── tables.css
        │   ├── js/
        │   │   ├── reload.js
        │   │   ├── script.js
        │   │   ├── script_enlaces.js
        │   │   └── SelectElementJS.js
        ├── vendor/
        │   └── ... (contenido de dependencias omitido)
        ├── index.php
        ├── composer.json
        ├── composer.lock
        ├── config.php
        ├── .gitignore
        ├── .htaccess
        ├── .env.desarrollo
        ├── .env.produccion
        └── LICENSE
        ```

---