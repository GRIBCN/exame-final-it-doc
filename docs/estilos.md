[⬅️ Volver a Inicio](index.md#documentación-del-proyecto-mvc-tienda) <!-- Enlace de regreso -->

---

# 🎨 Estilos CSS y Bootstrap

El proyecto utiliza un enfoque de diseño de tema oscuro para proporcionar una experiencia visual moderna y coherente. Los estilos están organizados en varios archivos CSS que gestionan diferentes componentes, asegurando modularidad y reutilización.

---

## 🌟 Uso General de Estilos

### 📁 Organización de los Archivos CSS

Los archivos CSS están ubicados en la carpeta `./public/css/`, y cada uno está dedicado a aspectos específicos del diseño:

- **`colors_backgrounds.css`**: Define los colores principales del fondo y del texto en el tema oscuro.
- **`alerts.css`**: Estilos personalizados para mensajes de alerta.
- **`buttons_Confirmar.css`**: Diseños para botones de acciones principales y secundarias.
- **`cards.css` y `cards_SmartGrid.css`**: Estilos para tarjetas y componentes relacionados.
- **`tables.css` y `table_SmartGrid.css`**: Estilos para tablas, incluyendo la tabla interactiva SmartGrid.
- **`select_filter.css`**: Estilos para los filtros dinámicos en los formularios.

---

## 🌌 Tema Oscuro

El proyecto utiliza un esquema de colores oscuros que mejora la legibilidad y minimiza la fatiga visual en condiciones de poca luz. El fondo es predominantemente negro o gris oscuro, mientras que los textos y elementos interactivos utilizan tonos claros para garantizar el contraste.

### 🎨 Ejemplo de Aplicación de Estilo General

??? example "Estilo General del Fondo y Texto"
    === "Código CSS"
    ```css title="colors_backgrounds.css"
    html, body {
        background-color: #121212; /* Fondo oscuro */
        color: #E0E0E0; /* Texto claro */
        font-family: 'Roboto', sans-serif;
    }
    ```

    === "Resultado"
    - **Fondo:** Un color oscuro (#121212) que minimiza la distracción.
    - **Texto:** Un color claro (#E0E0E0) para garantizar un contraste legible.
    - **Fuente:** `Roboto` como una fuente moderna y legible.

---

## 🛠️ Ejemplo de Componentes

### 🔔 Mensajes de Alerta

Los mensajes de alerta son diseñados para mostrar notificaciones o errores con un estilo distintivo.

??? example "Estilo de Alerta"
    === "Código CSS"
    ```css title="alerts.css"
    .alert-success {
        background-color: #28a745; /* Verde para éxito */
        color: white;
        padding: 20px;
        border-radius: 8px;
    }

    .alert-danger {
        background-color: #dc3545; /* Rojo para errores */
        color: white;
        padding: 20px;
        border-radius: 8px;
    }
    ```
    === "Resultado"
    - **Alertas Éxito:** Fondo verde brillante con texto blanco.
    - **Alertas Error:** Fondo rojo con texto blanco.

---

### 📋 Tablas Interactivas

Las tablas son uno de los componentes clave del proyecto, especialmente en la visualización de datos.

??? example "Estilo de Tablas"
    === "Código CSS"
    ```css title="table_SmartGrid.css"
    .table-smartgrid {
        background-color: #343a40; /* Fondo gris oscuro */
        color: white; /* Texto blanco */
        border-collapse: collapse;
    }

    .table-smartgrid th {
        background-color: #333333; /* Fondo para encabezados */
        color: #FFFFFF; /* Texto blanco */
        font-weight: bold;
    }

    .table-smartgrid td {
        background-color: #0f0f0f; /* Fondo para celdas */
        color: #E0E0E0; /* Texto claro */
    }
    ```

    === "Resultado"
    - **Encabezados:** Fondo gris oscuro con texto blanco en mayúsculas.
    - **Celdas:** Fondo negro con texto claro para maximizar la legibilidad.
    - **Interactividad:** Las filas cambian de color al pasar el cursor.

---

## 📦 Integración con Bootstrap

Bootstrap se utiliza en combinación con los estilos personalizados para aprovechar sus componentes predefinidos, como botones y modales, asegurando compatibilidad y rapidez en el diseño.

