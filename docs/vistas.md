[⬅️ Volver a Inicio](index.md#documentación-del-proyecto-mvc-enlaces) <!-- Enlace de regreso -->

---

# 👁️ Control de Vistas

En este apartado, exploraremos cómo se implementa el control de vistas en el proyecto **MVC EnlacesEnlaces de SOFTWARE**. Este control incluye desde el archivo principal `index.php` hasta los componentes que integran las vistas como el encabezado (`header.php`) y el pie de página (`footer.php`).

---

## 📄 Estructura de Control de Vistas

??? info "Arquitectura del Control de Vistas"
    === "Descripción"
    El control de vistas permite gestionar la representación de la interfaz de usuario de manera modular. Esto incluye:

    - **Activación del Autoload y Router desde `index.php`**: Maneja las peticiones y redirige a los controladores adecuados.
    - **`Autoload.php`**: Implementa la función `spl_autoload_register` para cargar automáticamente las clases necesarias.
    - **`Router.php`**: Gestiona las rutas y determina qué vista cargar según la URL.
    - **`ViewController.php`**: Controlador principal de vistas, responsable de la lógica para cargar los archivos correspondientes.
    - **`header.php` y `footer.php`**: Estructuras para el encabezado y pie de página.

---

## 🌟 Archivo Principal `index.php`

??? info "Punto de entrada principal"
    === "Código"
    ```php title="index.php"
    <?php
        require_once('config.php');
        require_once __DIR__ . '/vendor/autoload.php';

        use Dotenv\Dotenv;

        $envFile = getenv('APP_ENV') ?: 'desarrollo';
        $dotenv = Dotenv::createImmutable(__DIR__, ".env.$envFile");
        $dotenv->load();

        require_once('./controllers/Autoload.php');
        $autoload = new Autoload();

        $app = new Router();
    ?>
    ```

    === "Explicación"
    Este archivo actúa como el punto de entrada de la aplicación. Carga las configuraciones necesarias, las dependencias y utiliza el `Router` para manejar las solicitudes.

---

## 🔄 Clase `Autoload.php`

??? question "¿Qué hace `Autoload.php`?"
    === "Descripción"
    Esta clase implementa la función `spl_autoload_register` para cargar automáticamente las clases de modelos y controladores cuando son requeridas.

    === "Código"
    ```php title="Autoload.php"
    <?php
    class Autoload {
        public function __construct() {
            spl_autoload_register(function ($class_name) {
                $models_path = './models/' . $class_name . '.php';
                $controllers_path = './controllers/' . $class_name . '.php';

                if (file_exists($models_path)) require_once($models_path);
                if (file_exists($controllers_path)) require_once($controllers_path);
            });
        }
    }
    ?>
    ```

---

## 🔀 Clase `Router.php`

??? info "Manejo de Rutas"
    === "Descripción"
    La clase `Router` determina qué vista cargar según la URL o los datos recibidos por `GET` o `POST`. También filtra los datos para evitar ataques.

    === "Código"
    ```php title="Router.php"
    <?php
    class Router {
        public function __construct() {
            $route = $_GET['r'] ?? 'home';
            $controller = new ViewController();

            switch ($route) {
                case 'home':
                    $controller->load_view('home');
                    break;
                default:
                    $controller->load_view('404');
                    break;
            }
        }
    }
    ?>
    ```

---

## 📄 Clase `ViewController.php`

??? info "Controlador de Vistas"
    === "Descripción"
    Este controlador maneja la lógica para cargar vistas específicas según las rutas definidas en el `Router`.

    === "Código"
    ```php title="ViewController.php"
    <?php
    class ViewController {
        public function load_view($view) {
            include_once './views/header.php';
            include_once "./views/{$view}.php";
            include_once './views/footer.php';
        }
    }
    ?>
    ```

---

## 🖼️ Componentes de la Vista

### 🌟 `header.php`

??? info "Encabezado de las páginas"
    === "Código"
    ```php title="header.php"
    <?php
    $template = '
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>%s</title>
            <link rel="stylesheet" href="./public/css/styles.css">
        </head>
        <body>
            <header class="header">
                <h1>%s</h1>
            </header>
            <main class="main">
    ';
    printf($template, APP_TITLE, APP_TITLE);
    ?>
    ```

    === "Explicación"
    El archivo `header.php` genera el encabezado HTML para todas las páginas, cargando los estilos necesarios y configurando el título dinámicamente.

---

### 🌟 `footer.php`

??? info "Pie de página de las vistas"
    === "Código"
    ```php title="footer.php"
    <?php 
    print('
            </main>
            <footer class="footer">
                <p>© 2024 EnlacesEnlaces de SOFTWARE MVC. Todos los derechos reservados.</p>
            </footer>
        </body>
        </html>
    ');
    ?>
    ```

    === "Explicación"
    Este archivo completa la estructura HTML de la página, añadiendo un pie de página básico con información de derechos reservados.

---

## 🌐 Consideraciones

1. **Modularidad**: El uso de componentes como `header.php` y `footer.php` facilita la consistencia en el diseño de la aplicación.
2. **Cargadores Automáticos**: `Autoload.php` asegura que las clases necesarias se carguen dinámicamente, optimizando el flujo de trabajo.
3. **Gestión de Rutas**: `Router.php` simplifica el manejo de solicitudes, conectando las rutas con las vistas correspondientes.

---
