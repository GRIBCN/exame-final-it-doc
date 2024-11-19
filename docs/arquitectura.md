[⬅️ Volver](index.md#documentación-del-proyecto-mvc-enlaces) <!-- Enlace de regreso -->

---

# 📜 Descripción de la Arquitectura MVC
---

La arquitectura Modelo-Vista-Controlador (MVC) es un patrón de diseño ampliamente utilizado en el desarrollo de aplicaciones web. Este modelo separa la lógica del negocio, la interfaz de usuario y la manipulación de datos, permitiendo un desarrollo modular, escalable y más fácil de mantener.

En el contexto del proyecto **MVC Enlaces de SOFTWARE**, la estructura del proyecto sigue las mejores prácticas para implementar MVC de manera eficiente, con una clara separación de responsabilidades.

---

## 📋 Beneficios de la Arquitectura MVC
---

- **Modularidad**: Separación clara de responsabilidades.
- **Escalabilidad**: Facilita agregar nuevas funcionalidades.
- **Mantenibilidad**: El código es más fácil de entender y modificar.
- **Reutilización de Código**: Componentes como vistas y modelos pueden ser reutilizados en diferentes partes del proyecto.

??? info "Ejemplo Práctico"
    === "Código"
        ```php title="index.php"
        <?php
        require_once('config.php');
        require_once __DIR__ . '/vendor/autoload.php';

        use Dotenv\Dotenv;

        // Detectar el entorno actual
        $envFile = getenv('APP_ENV') ?: 'desarrollo';

        // Validar el entorno
        $validEnvs = ['desarrollo', 'produccion'];
        if (!in_array($envFile, $validEnvs)) {
            die("Entorno no válido: $envFile");
        }

        // Cargar el archivo .env según el entorno
        $dotenv = Dotenv::createImmutable(__DIR__, ".env.$envFile");
        $dotenv->load();

        // Definir las variables cargadas desde .env
        define('BASE_URL', $_ENV['BASE_URL']);

        // Definir las variables de acceso a la BD
        define('DB_HOST', $_ENV['DB_HOST']);
        define('DB_USER', $_ENV['DB_USER']);
        define('DB_PASS', $_ENV['DB_PASSWORD']);
        define('DB_NAME', $_ENV['DB_NAME']);

        require_once('./controllers/Autoload.php');

        $autoload = new Autoload();

        $app = new Router();
        ?>
        ```

    === "Explicación"
        En este ejemplo:
        
        - El archivo `index.php` se utiliza como el punto de entrada principal de la aplicación.
        - Utiliza la clase `Dotenv` para cargar las configuraciones del entorno.
        - Define constantes para las variables de conexión a la base de datos.
        - Carga la clase `Autoload` para la carga automática de los controladores y modelos.
        - Finalmente, instancia la clase `Router` para manejar las rutas de la aplicación.

    === "Arquitectura"
        - **Controlador**: El controlador `Router.php` maneja la lógica de enrutamiento y redirige a las vistas o controladores específicos.
        - **Vista**: Se cargan vistas específicas como `home.php` o `404.php` según la ruta.
        - **Modelo**: Los modelos no están directamente invocados en este archivo, pero el `Router` los utiliza según las necesidades.

---

[⬆️ Subir](#) <!-- Enlace para regresar al inicio de la página -->
