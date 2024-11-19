[⬅️ Volver a Inicio](index.md#documentación-del-proyecto-mvc-enlaces) <!-- Enlace de regreso -->

---

# 📜 La Parte de JavaScript y AJAX

JavaScript se utiliza en este proyecto para manejar la interactividad y el dinamismo en la aplicación. Este lenguaje permite que las vistas respondan a las acciones del usuario sin necesidad de recargar la página, proporcionando una experiencia más fluida y eficiente.

En particular, este proyecto hace uso extensivo de **AJAX** para realizar solicitudes al servidor y manipular dinámicamente el DOM con los datos devueltos. Además, se ha implementado una clase personalizada (`SelectElementJS`) para la creación dinámica de elementos HTML, como etiquetas `<select>`.

---

## 🌟 Uso General de JavaScript en el Proyecto

El proyecto utiliza JavaScript para las siguientes tareas principales:

1. **Interactividad del Usuario**:
   - Escucha de eventos como `click` y `change` en botones, inputs y radio buttons.
   - Actualización dinámica del contenido en las vistas.

2. **Manipulación del DOM**:
   - Generación dinámica de elementos HTML (por ejemplo, `<select>`).
   - Renderización de mensajes y tablas actualizadas.

3. **Solicitudes AJAX**:
   - Comunicación con el servidor para ejecutar operaciones específicas sin recargar la página.
   - Actualización de datos en las vistas basándose en las respuestas del servidor.

---

## 🛠️ Ejemplo de Llamada AJAX

??? example "Llamada AJAX para Filtrar Enlaces"
    === "Código JS"
    ```javascript title="script_enlaces.js"
    fetch('index.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'X-Requested-With': 'XMLHttpRequest'
        },
        body: new URLSearchParams({
            'views': 'enlaces',
            'crud': 'filter',
            'r': 'enlaces-filter',
            'consulta': searchConsulta,
            'field': searchField,
            'value': searchValue
        })
    })
    .then(response => response.json()) // Procesar la respuesta JSON
    .then(data => {
        if (data.success) {
            // Actualizar la tabla con los datos recibidos
            tablaContainer.innerHTML = data.tablaHTML;

            // Mostrar mensaje de éxito
            const mensajeSuccess = `
                <strong>Éxito: </strong> 
                ${data.msg01} 
                <strong> "${data.msg02}" </strong>
                ${data.msg03}
            `;
            mensajeStatus.innerHTML = htmlMessageZone('success', mensajeSuccess);
        } else {
            // Mostrar mensaje de error
            mensajeStatus.innerHTML = htmlMessageZone('danger', data.msg01);
        }
    })
    .catch(error => {
        // Manejo de errores en caso de fallo en la solicitud AJAX
        mensajeStatus.innerHTML = htmlMessageZone('danger', 'Error al procesar la solicitud.');
    });
    ```
    === "Explicación"
    En este ejemplo, se realiza una llamada al servidor para filtrar enlaces en la tabla basándose en los criterios seleccionados por el usuario:
    - **Método `POST`**: Se envían datos al servidor para procesar la solicitud.
    - **Respuestas JSON**: La respuesta del servidor se interpreta como JSON, y los datos recibidos se utilizan para actualizar dinámicamente el DOM.

---

## ✨ Generación Dinámica de Elementos

El proyecto incluye una clase personalizada, `SelectElementJS`, para generar dinámicamente etiquetas `<select>`. Esta clase permite crear elementos con múltiples opciones y atributos según las necesidades de la aplicación.

??? example "Uso de la Clase SelectElementJS"
    === "Código JS"
    ```javascript title="SelectElementJS.js"
    const selectElement = new SelectElementJS('idDynamicSelect', 'dynamicSelect', 'form-select', true);
    selectElement.setDefaultOption('Seleccione una opción...', 'default');
    selectElement.addOption('valor1', 'Opción 1');
    selectElement.addOption('valor2', 'Opción 2', true); // Opción seleccionada por defecto

    // Renderizar el <select> y añadirlo al DOM
    document.getElementById('contenedorSelect').innerHTML = selectElement.render();
    ```
    === "Resultado"
    Este código genera dinámicamente un elemento `<select>` con las opciones especificadas y lo agrega al contenedor correspondiente en el DOM.

---

## 🖥️ Ejemplo Práctico: Recarga de Página

??? example "Función para Recargar la Página"
    === "Código JS"
    ```javascript title="reload.js"
    function reloadPage(url) {
        url = "index.php?r=" + url;
        console.log('Redirigiendo a:', url);
        setTimeout(function () {
            window.location.href = url;
        }, 3000);
    }
    ```
    === "Explicación"
    Esta función se utiliza para redirigir al usuario a una nueva página después de un breve retraso, proporcionando una experiencia controlada y fluida.

---

## 📋 Resumen de Funcionalidades

1. **AJAX**:
   - Manejo eficiente de solicitudes al servidor y actualización del DOM en tiempo real.
   - Mejora la experiencia del usuario al evitar recargas completas de la página.

2. **Dinamismo con `SelectElementJS`**:
   - Creación flexible y reutilizable de elementos HTML dinámicos, como `<select>`.

3. **Modularidad**:
   - Los archivos JS están organizados según su funcionalidad (`reload.js`, `script_enlaces.js`, etc.), lo que facilita el mantenimiento y la escalabilidad.

---
