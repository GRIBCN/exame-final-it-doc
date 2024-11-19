## 📂 Estructura General del Proyecto
---

El proyecto **MVC Tienda** está organizado en varias carpetas principales que corresponden a los tres componentes del patrón MVC y otros elementos esenciales. A continuación, se describe cada sección.

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
        c:/servidor/www/examen-final-tienda/
        ├── controllers/
        │   ├── Router.php
        │   ├── TiendaController.php
        │   └── ViewController.php
        ├── models/
        │   └── Model_crud.php
        ├── views/
        │   ├── header.php
        │   ├── footer.php
        │   └── home.php
        ├── public/
        │   ├── css/
        │   │   └── styles.css
        │   ├── js/
        │   │   └── script.js
        ├── vendor/
        ├── index.php
        ├── .env
        └── composer.json
        ```

---