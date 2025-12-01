# Retrospectiva - Iteración 1

**Fecha:** 19/11/2025
**Participantes:** Gonzalo Aquino

---

## Resumen de la Iteración
El objetivo principal de esta iteración fue establecer el Producto Mínimo Viable (MVP) enfocado en la gestión de clientes y la generación de una factura individual.

Para cumplir con los requisitos, se implementó una arquitectura **Web API utilizando Spring Boot**, separando claramente el Backend del Frontend, esta decisión permitió entregar un producto moderno, escalable y alineado con los estándares actuales de desarrollo Java.

**Estado final:** 100% de las Historias de Usuario planificadas (HU-01 a HU-06) fueron completadas y verificadas funcionalmente.

---

## ¿Qué funcionó bien?

* **Arquitectura Spring Boot:** La configuración inicial del proyecto (Web, JPA, Lombok) fue exitosa, permitiendo un desarrollo ágil de las capas de Controlador, Servicio y Repositorio.
* **Modelo de Datos:** El mapeo de las entidades (`Cliente`, `Cuenta`, `Servicio`, `Factura`) y sus relaciones (`@OneToMany`, `@ManyToMany`) funcionó correctamente, soportando la lógica de negocio sin problemas.
* **Integración Frontend-Backend:** Se logró conectar exitosamente la interfaz web (HTML/CSS/JS) con la API REST. El uso de `fetch` en JavaScript permitió una experiencia de usuario fluida (SPA) sin recargas de página.
* **Herramientas de Verificación:** La incorporación de **Postman** para probar los endpoints antes de conectar el frontend y el uso de la **Consola H2** para validar los datos en memoria fueron clave para detectar errores rápidamente.

---

## ¿Qué no funcionó o quedó pendiente?

* **Persistencia volátil:** Al utilizar la base de datos H2 en modo memoria (`mem:testdb`), los datos se pierden al reiniciar el servidor, esto requiere cargar scripts SQL manualmente en cada sesión de desarrollo.
* **Funcionalidad de UI secundaria:** En el frontend los botones "Gestión de Catálogo" y "Salir" se implementaron visualmente pero no tienen funcionalidad asociada todavía, se decidió priorizar el Happy Path de facturación.
* **Feedback de errores al usuario:** Si bien el sistema captura errores, la interfaz de usuario aún muestra alertas básicas (`alert()`) en lugar de mensajes integrados o notificaciones más amigables.

---

## Retos y Desafíos

Durante el desarrollo enfrenté desafíos técnicos específicos que sirvieron de aprendizaje:

1.  **Gestión de Puertos y Procesos:**
    * *El Problema:* Errores recurrentes de "Port 8080/8081 already in use" al intentar reiniciar la aplicación.
    * *La Causa:* Procesos de Java quedaban "huérfanos" al cerrar el editor sin detener el servidor explícitamente.
    * *La Solución:* Adoptar la disciplina de detener el servidor (`Stop`) desde el IDE antes de cerrar, y el uso de herramientas del sistema para liberar puertos bloqueados.

2.  **Serialización JSON:**
    * *El Problema:* Al consultar datos, la aplicación fallaba con un "StackOverflowError" o JSON malformado.
    * *La Causa:* La relación bidireccional entre `Cliente` y `Cuenta` generaba un bucle infinito al intentar convertir los objetos a texto.
    * *La Solución:* Uso de la anotación `@JsonIgnore` en el lado inverso de la relación para cortar el ciclo durante la serialización.

3.  **Configuración de Base de Datos:**
    * *El Problema:* Dificultad inicial para conectar la consola H2 con la base de datos de la aplicación.
    * *La Solución:* Ajuste de la URL JDBC en `application.properties` y en la consola para asegurar que ambas apunten a la misma instancia en memoria.

4.  **Control de Visibilidad en Frontend:**
    * *El Problema:* El modal de confirmación aparecía visible al cargar la página debido a conflictos de CSS.
    * *La Solución:* Ajuste de las clases CSS para garantizar que los elementos inicien ocultos y sean controlados exclusivamente por la lógica de JavaScript.

---

## Plan de Mejoras para la Iteración 2

Para la siguiente fase del proyecto, se implementarán las siguientes mejoras en el proceso:

* **Ciclo de Vida del Servidor:** Mantener un control estricto sobre el inicio y parada del servidor Spring Boot para evitar tiempos muertos por bloqueo de puertos.
* **Modularización del Frontend:** A medida que la interfaz crezca con Facturación Masiva, se buscará organizar mejor el código JavaScript para no tener un solo archivo `app.js` gigante.
* **Manejo de Excepciones:** Refinar el Backend para devolver códigos de estado HTTP precisos y mensajes de error claros que el Frontend pueda mostrar al usuario.

---