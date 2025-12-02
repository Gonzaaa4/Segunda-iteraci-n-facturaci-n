# Documento de Diseño y Planificación - Iteración 2

---

## Trabajo en equipo

Este proyecto continúa siendo desarrollado de manera individual por **Gonzalo Aquino**, manteniendo los roles de Full Stack Developer y Analista Funcional.

---

## Diseño OO (Ampliación del Modelo)


**Cambios principales en el Modelo:**
1.  **Refactorización de Factura:** Se agregan campos para controlar el estado del pago (`saldoPendiente`, `pagada`).
2.  **Nueva Entidad `ProcesoMasivo`:** Para cumplir con HU-08 (Registro de ejecuciones). Guarda la fecha y cuántas facturas generó.
3.  **Nueva Entidad `Pago`:** Para cumplir con HU-09 y HU-10. Registra fecha, monto y medio de pago, y se relaciona con una `Factura`.
4.  **Nueva Entidad `NotaCredito`:** Para cumplir con HU-11 (Anulación).


![alt text](<Diagrama de clases Iteracion2.png>)

---

## Wireframe y caso de uso 

### Caso de Uso 1: Ejecutar Facturación Masiva
Basado en: (2)Iteracion2.png Historias de Usuario: HU-07 y HU-08.

Actor: Usuario Administrativo.

Descripción: El usuario dispara el proceso automático para generar facturas a todas las cuentas que se encuentren en estado "ACTIVA" para un período determinado.

Precondiciones: Deben existir cuentas con estado ACTIVA y servicios asociados en la base de datos.

Flujo Principal:

El usuario selecciona la opción "Facturación Masiva" en el menú lateral.

El sistema muestra el panel de facturación masiva.

El usuario ingresa el período a facturar (ej. "11/2025") en el campo de texto.

El usuario hace clic en el botón "Ejecutar Proceso".

El sistema procesa internamente todas las cuentas activas.

Resultado (Ver imagen): El sistema muestra un panel de resumen ("Proceso Finalizado") indicando:

Fecha y hora de ejecución.

Cantidad de facturas generadas.

Monto total facturado ($).

Observaciones del proceso.

### Caso de Uso 2: Registrar Pago (Total o Parcial)
Basado en: (3)Iteracion2.png Historias de Usuario: HU-09 y HU-10.

Actor: Usuario Administrativo.

Descripción: El usuario registra el ingreso de dinero imputado a una factura específica, pudiendo ser un pago total o parcial.

Precondiciones: El cliente debe existir y tener cuentas con facturas emitidas (se requiere conocer el ID de la factura).

Flujo Principal:

El usuario navega a "Gestión de Clientes" y busca un cliente por CUIT.

El usuario selecciona una cuenta del menú desplegable "Seleccione Cuenta".

El sistema habilita los botones de acción.

El usuario hace clic en el botón verde "Registrar Pago (HU-09)".

Resultado (Ver imagen): El sistema despliega una ventana modal "Registrar Pago".

El usuario ingresa:

ID de Factura: El número identificador de la factura a pagar.

Monto: La cantidad de dinero a abonar.

Medio de Pago: Selecciona una opción (Efectivo, Transferencia, etc.).

El usuario hace clic en "Confirmar Pago".

El sistema valida que el monto no exceda la deuda y registra el pago.

El sistema muestra una alerta confirmando el éxito de la operación y cierra el modal.

Flujo Alternativo (Error de Validación):

3a. Si el usuario intenta pagar un monto mayor al saldo pendiente de la factura, el sistema muestra un mensaje de error: "El monto excede el saldo pendiente" y no registra el pago.

### Caso de Uso 3: Anular Factura (Excepciones)
(Aunque no está en las capturas, es parte del flujo complementario a los Pagos) Historias de Usuario: HU-11.

Actor: Usuario Administrativo.

Descripción: El usuario cancela una factura emitida erróneamente, generando una Nota de Crédito.

Flujo Principal:

El usuario presiona el botón rojo "Anular Factura (HU-11)".

El sistema despliega el modal de anulación (borde rojo).

El usuario ingresa el ID de la factura.

El usuario confirma la acción.

El sistema cambia el estado de la factura a ANULADA, pone el saldo en 0 y genera la Nota de Crédito correspondiente.

![alt text]((2)Iteracion2.png)
![alt text]((3)Iteracion2.png)

---

## Backlog de Iteración 2

Objetivo: Completar el ciclo comercial y automatizar procesos.

| ID | Historia de Usuario | Descripción Breve |
| :--- | :--- | :--- |
| **HU-07** | Facturación Masiva | Generar facturas para TODAS las cuentas activas en un solo clic. |
| **HU-08** | Historial de Ejecuciones | Consultar cuándo se corrió la facturación masiva y con qué resultado. |
| **HU-09** | Pago Total | Registrar el pago completo de una factura. |
| **HU-10** | Pago Parcial | Registrar un pago a cuenta, dejando saldo pendiente. |
| **HU-11** | Anulación | Anular una factura emitida generando una Nota de Crédito. |

---

## Tareas Técnicas (Plan de Trabajo)

**Fase 1: Automatización (Facturación Masiva)**
* [ ] **T-20:** Crear entidad `ProcesoMasivo` (log de ejecución).
* [ ] **T-21:** Crear `ProcesoMasivoRepository`.
* [ ] **T-22:** Implementar lógica en `FacturacionService` para iterar cuentas activas y generar facturas en lote.
* [ ] **T-23:** Crear endpoint `POST /api/facturacion/masiva` en `FacturacionController`.
* [ ] **T-24:** Frontend: Agregar pantalla/botón para disparar la facturación masiva y ver el resultado.

**Fase 2: Gestión de Pagos (Refactor)**
* [ ] **T-25:** Modificar entidad `Factura` para agregar campo `saldo` y `estado` (PAGADA/PENDIENTE).
* [ ] **T-26:** Crear entidad `Pago` (fecha, monto, factura_id).
* [ ] **T-27:** Crear `PagoRepository`.
* [ ] **T-28:** Implementar lógica en `PagoService` (validar monto, descontar saldo de factura).
* [ ] **T-29:** Crear `PagoController`.
* [ ] **T-30:** Frontend: Agregar opción de "Registrar Pago" en la visualización del cliente.

**Fase 3: Anulación (Excepciones)**
* [ ] **T-31:** Crear entidad `NotaCredito` (vinculada a una Factura original).
* [ ] **T-32:** Lógica para anular factura (dejar saldo en 0 y crear NC).
* [ ] **T-33:** Frontend: Botón de "Anular" en el historial del cliente.