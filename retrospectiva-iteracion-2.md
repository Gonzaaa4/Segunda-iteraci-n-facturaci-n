# Retrospectiva - Iteración 2 (Final)

**Fecha:** 03/12/2025
**Participante:** Gonzalo Aquino (Desarrollo Individual)

---

## 1. Resumen del Hito
El objetivo de esta segunda iteración fue transformar el sistema de un simple emisor de facturas a un **ERP (Sistema de Planificación de Recursos) completo**, cerrando el ciclo comercial y administrativo.

Se integraron funcionalidades complejas de automatización (**Facturación Masiva**) y gestión financiera (**Pagos y Anulaciones**). El sistema ahora cumple con el 100% de los requisitos funcionales, permitiendo gestionar deudas, saldos pendientes y correcciones, manteniendo la arquitectura base de Spring Boot establecida en la etapa anterior.

---

## 2. ¿Qué funcionó bien? (Logros)

* **Lógica de Negocio Robusta:** La implementación de servicios transaccionales (`@Transactional`) para la Facturación Masiva y los Pagos garantizó la integridad de los datos. Si un pago falla, el saldo de la factura no se toca.
* **Manejo de Dinero:** El uso estricto de `BigDecimal` para todos los cálculos monetarios (totales, saldos, pagos parciales) evitó errores de precisión decimal típicos en sistemas financieros.
* **Interfaz de Usuario (SPA):** A pesar de no utilizar frameworks frontend complejos, se logró una experiencia de usuario fluida ("Single Page Application") mediante el uso de JavaScript asíncrono (`fetch`) y ventanas modales, evitando recargas de página innecesarias.
* **Gestión de Excepciones:** La decisión de manejar la anulación mediante **Notas de Crédito** (en lugar de borrar registros) demuestra un entendimiento correcto de las reglas de negocio y contabilidad.

---

## 3. Retos y Desafíos (Problemas Solucionados)

Durante esta etapa, la complejidad técnica aumentó y surgieron desafíos específicos:

### A. Referencias Circulares (El "Bucle Infinito" JSON)
* **El Problema:** Al intentar listar los datos del cliente en el frontend, la aplicación fallaba o el navegador se colgaba.
* **La Causa:** La relación bidireccional entre `Cliente` (que tiene una lista de Cuentas) y `Cuenta` (que tiene un Cliente) generaba una recursión infinita al intentar serializar los objetos a JSON.
* **La Solución:** Se diagnosticó inspeccionando la respuesta de red y se solucionó aplicando la anotación `@JsonIgnore` en la entidad hija (`Cuenta`), cortando el ciclo de serialización.

### B. Conflictos de Anidamiento en el DOM
* **El Problema:** Los paneles nuevos (Facturación Masiva y Pagos) no se visualizaban correctamente o desaparecían al navegar entre pestañas.
* **La Causa:** Un error estructural en el HTML donde los modales y paneles nuevos fueron colocados accidentalmente *dentro* de contenedores que se ocultaban mediante CSS (`display: none`).
* **La Solución:** Se refactorizó el archivo `index.html` para "aplanar" la estructura, asegurando que todos los paneles principales y modales sean elementos hermanos independientes.

### C. Persistencia Volátil (H2)
* **El Desafío:** Al utilizar una base de datos en memoria para desarrollo, cada reinicio del servidor borraba los datos de prueba.
* **La Adaptación:** Esto obligó a crear scripts SQL de "semilla" (Seed Data) robustos para poder recrear escenarios complejos (ej. tener una factura lista para pagar) rápidamente tras cada reinicio.

---

## 4. Lecciones Aprendidas

1.  **Validación Frontend vs Backend:** Aprendí que no basta con ocultar un botón en el HTML; el Backend siempre debe validar las reglas de negocio (ej. rechazar un pago si el monto excede el saldo), ya que las peticiones pueden llegar por fuera de la interfaz (Postman).
2.  **Sincronización:** Es vital asegurar que los elementos del DOM existan antes de que el JavaScript intente asignarles eventos.
3.  **Arquitectura Limpia:** Mantener los Controladores "delgados" (solo recibiendo HTTP) y la lógica pesada en los Servicios facilitó mucho la implementación de la Facturación Masiva.

---

## 5. Deuda Técnica y Mejoras Futuras

Si el proyecto continuara a una fase productiva, se deberían abordar los siguientes puntos:

* **Persistencia Real:** Migrar de H2 a un motor persistente como MySQL o PostgreSQL.
* **Seguridad:** Implementar Spring Security para manejo de sesiones y roles.
* **Reportes:** Generación de PDFs para las Facturas y Recibos de Pago.

---