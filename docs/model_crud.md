[⬅️ Volver a Inicio](index.md#documentación-del-proyecto-mvc-enlaces) <!-- Enlace de regreso -->

---

# 🗂️ Componentes Específicos del Modelo MVC. La Clase `Model_crud`

Este apartado describe cómo la clase `Model_crud` implementa operaciones generales de base de datos en el proyecto **MVC Enlaces de SOFTWARE**. Esta clase se utiliza como base para crear modelos específicos que interactúan con vistas, controladores y la base de datos.

---

## 📌 Función de la Clase `Model_crud`

??? info "¿Qué es y cómo funciona?"
    === "Descripción"
    La clase `Model_crud` es una clase abstracta que proporciona una interfaz generalizada para las operaciones CRUD (Create, Read, Update, Delete). Utiliza **MySQLi** para realizar consultas preparadas de manera segura, minimizando riesgos de inyección SQL.

    === "Responsabilidades principales"
    - **Conexión a la base de datos**: Maneja la apertura y cierre de la conexión.
    - **Consultas preparadas**: Ejecuta consultas de forma segura utilizando métodos como `execute_prepared_query` y `execute_prepared_select`.
    - **Métodos CRUD generalizados**: Incluye métodos como `insert`, `update`, `delete` y `get` para manejar datos.

---

## 🌟 Estructura de la Clase `Model_crud`

??? info "Código principal"
    === "Código"
    ```php title="Model_crud.php"
    abstract class Model_crud {
        private static $db_host = DB_HOST;
        private static $db_user = DB_USER;
        private static $db_pass = DB_PASS;
        private static $db_name = DB_NAME;

        protected $table = '';    // Nombre de la tabla
        protected $column_id = ''; // Nombre de la columna clave

        public function insert($data) { /* Inserción genérica */ }
        public function update($id, $data) { /* Actualización genérica */ }
        public function delete($id) { /* Eliminación genérica */ }
        public function get($id = null) { /* Recuperación genérica */ }
    }
    ```

    === "Explicación"
    Esta clase define métodos genéricos para realizar operaciones en cualquier tabla. Las subclases especifican el nombre de la tabla (`$table`) y su clave primaria (`$column_id`).

---

## 🔧 Subclases de `Model_crud`

Las subclases especializan el comportamiento de `Model_crud` para una tabla o vista específica. En este proyecto, la clase `EnlacesController` hereda de `Model_crud` y opera sobre la vista `vista_enlaces`.

??? info "Subclase: `EnlacesController`"
    === "Código"
    ```php title="EnlacesController.php"
    class EnlacesController extends Model_crud {
        protected $table = 'vista_enlaces';
        protected $column_id = 'rowid';

        public function getValueFields($field) {
            $query = "CALL enlaces_field_DISTINCT_START(?)";
            return $this->execute_prepared_select($query, 's', [$field]);
        }

        public function filterEnlaces($query, $valor) {
            return $this->execute_prepared_select($query, 's', ['%' . $valor . '%']);
        }
    }
    ```

    === "Explicación"
    - **`getValueFields($field)`**: Obtiene valores únicos de una columna específica usando procedimientos almacenados.
    - **`filterEnlaces($query, $valor)`**: Filtra los resultados de la vista `vista_enlaces` con base en una consulta y un valor.

---

## 📂 Estructura de la Vista `vista_enlaces`

??? info "Vista de base de datos"
    === "Código SQL"
    ```sql title="vista_enlaces"
    CREATE VIEW vista_enlaces AS
    SELECT 
        ROW_NUMBER() OVER (ORDER BY a.pk_categoria, b.pk_vinculo) AS rowid,
        pk_categoria,
        tipo, 
        categoria,
        pk_vinculo, 
        titulo, 
        enlace, 
        fk_categoria
    FROM categoria a
    INNER JOIN vinculos b ON b.fk_categoria = a.pk_categoria
    ORDER BY tipo, categoria, titulo;
    ```

    === "Explicación"
    - **`rowid`**: Identificador incremental único generado para cada fila.
    - **Relación entre `categoria` y `vinculos`**: Une las tablas relacionadas para formar la vista.
    - **Ordenamiento**: Organiza los resultados por tipo, categoría y título.

    === "Ejemplo de datos"
    ![Vista de la tabla `vista_enlaces`](assets/DB_view.png)

---

## 🔧 Procedimientos Almacenados para Filtros

??? info "Procedimientos almacenados"
    === "Código SQL"
    ```sql title="Procedimiento: enlaces_field_DISTINCT_START"
    DELIMITER $$

    CREATE PROCEDURE enlaces_field_DISTINCT_START (
        IN field VARCHAR(254)
    )
    BEGIN
        DROP TEMPORARY TABLE IF EXISTS temp_field;
        CREATE TEMPORARY TABLE temp_field (
            f_field_orign VARCHAR(254),
            f_field VARCHAR(254),
            f_order INT
        );
        
        -- Llamamos a la función de generación de lista
        CALL enlaces_field_DISTINCT(field);
        
        -- Devolvemos los valores únicos
        SELECT DISTINCT f_field FROM temp_field WHERE f_field <> '' ORDER BY f_field;
    END$$

    DELIMITER ;
    ```
    === "Explicación"
    Este procedimiento permite generar una lista de valores únicos de cualquier columna de la vista `vista_enlaces`. Se utiliza en el método `getValueFields`.

---

## 🌟 Ejemplo Práctico

??? example "Operación CRUD: Filtrar enlaces por categoría"
    === "Código"
    ```php title="Ejemplo de filtrado por categoría"
    $enlacesController = new EnlacesController();
    $enlaces = $enlacesController->filterEnlaces(
        "SELECT * FROM vista_enlaces WHERE categoria LIKE ?", "CSS"
    );

    print_r($enlaces);
    ```

    === "Salida esperada"
    ```plaintext
    Array
    (
        [0] => Array
            (
                [rowid] => 1
                [pk_categoria] => 3
                [tipo] => LENGUAJE
                [categoria] => CSS
                [pk_vinculo] => 4
                [titulo] => Koala
                [enlace] => http://koala-app.com/
            )
    )
    ```

    === "Explicación"
    - La consulta filtra enlaces con la categoría `CSS`.
    - Devuelve un arreglo asociativo con los enlaces que cumplen la condición.

---

## 🧩 Ventajas de la Implementación

1. **Reutilización**: La clase `Model_crud` permite manejar cualquier tabla o vista de forma genérica.
2. **Seguridad**: Las consultas preparadas protegen contra inyecciones SQL.
3. **Escalabilidad**: Los métodos específicos, como `filterEnlaces`, pueden extenderse fácilmente para nuevos requerimientos.
4. **Modularidad**: Siguiendo el patrón MVC, el modelo mantiene una separación clara de las responsabilidades.

---
