# Documento de Diseño y Planificación - Iteración 1

---

## Trabajo en equipo

Este proyecto es desarrollado de manera individual, he asumido todos los roles del ciclo de vida de desarrollo para esta iteración:

* **Gonzalo Aquino:**
    * **Análisis:** Definición de requisitos (HU-01 a HU-06) y modelado del dominio.
    * **Backend:** Implementación de la API REST utilizando Java y Spring Boot, configuración de base de datos H2.
    * **Frontend:** Desarrollo de la interfaz web con HTML5, CSS3 y JavaScript vanilla para consumir la API.
    * **QA:** Pruebas manuales de endpoints con Postman y verificación de flujo de usuario en el navegador.

---

## Diseño OO (Arquitectura Modelo Vista Controlador - Spring Boot)

El diseño ha evolucionado de un modelo simple de clases a una arquitectura en capas soportada por **Spring Boot**, se separaron las responsabilidades en:
1.  **Modelo:** Clases persistentes que mapean a la base de datos (JPA).
2.  **Repositorios:** Interfaces para el acceso a datos.
3.  **Servicios:** Lógica de negocio (Cálculos, validaciones, generación de facturas).
4.  **Controladores:** API REST que expone la funcionalidad a la web.


![Diagrama de Clases Iteración 1]![alt text](DiagramaClasesIteracion1(2)-1.png)

---

## Wireframe y Caso de Uso

![alt text](Wireframe1.jpeg)

![alt text](Wireframe2.jpeg)

**Caso de Uso Implementado: Generar Factura Individual (HU-05, HU-06)**

* **Actor:** Usuario Administrativo.
* **Objetivo:** Buscar un cliente, seleccionar una cuenta activa y generar su factura.
* **Flujo (Frontend):**
    1.  El usuario ingresa el CUIT en el buscador y presiona "Buscar".
    2.  El sistema consulta a la API (`GET /api/clientes/{cuit}`) y muestra los datos del cliente y sus cuentas.
    3.  El usuario selecciona una cuenta del menú desplegable.
    4.  El sistema muestra los servicios contratados asociados a esa cuenta.
    5.  El usuario presiona el botón **"Generar Factura Individual"**.
    6.  El sistema envía la petición (`POST /api/facturacion...`), calcula totales en el backend y devuelve el objeto Factura.
    7.  Se muestra un **Modal (Pop-up)** confirmando el éxito y mostrando el número de factura y el monto total calculado.

---

## Backlog de Iteración 1

Se han completado todas las historias de usuario planificadas para esta iteración.

| ID | Historia de Usuario | Estado | Entregable Técnico |
| :--- | :--- | :--- | :--- |
| **HU-01** | ABM de Clientes | **Completado** | `ClienteController`, `ClienteService`, `index.html` |
| **HU-02** | Gestión de Cuentas | **Completado** | Relación `@OneToMany` Cliente-Cuenta |
| **HU-03** | Catálogo de Servicios | **Completado** | Entity `Servicio` y Repository (Backend) |
| **HU-04** | Contratar Servicios | **Completado** | Relación `@ManyToMany` Cuenta-Servicio |
| **HU-05** | Facturación Individual | **Completado** | Endpoint `POST .../generar`, lógica en Service |
| **HU-06** | Cálculo de Totales e IVA | **Completado** | Método `calcularTotales()` en Entidad Factura |

---

## Tareas Técnicas

Lista de tareas ejecutadas para cumplir con el backlog.

**Configuración y Modelo Base**
* [x] **T-00:** Inicializar proyecto Spring Boot (Web, JPA, H2, Lombok).
* [x] **T-01:** Definir Enum `CondicionFiscal`.
* [x] **T-02:** Implementar Entity `Cliente` con JPA.
* [x] **T-03:** Definir Enum `EstadoCuenta`.
* [x] **T-04:** Implementar Entity `Cuenta` y relación con Cliente.

**Lógica de Negocio y Persistencia**
* [x] **T-06:** Crear `ClienteRepository` y `ClienteService` (Lógica ABM).
* [x] **T-08:** Implementar Entity `Servicio`.
* [x] **T-10:** Establecer relación N-a-N entre `Cuenta` y `Servicio`.

**Facturación (Core)**
* [x] **T-11:** Implementar Entity `ItemFactura` (Snapshot de precio).
* [x] **T-12:** Implementar Entity `Factura`.
* [x] **T-14:** Crear `FacturacionService` con método `generarFacturaIndividual()`.
* [x] **T-15:** Implementar lógica de cálculo de totales e IVA en la clase `Factura`.

**Interfaz y API (Frontend & Controller)**
* [x] **T-17a:** Crear `ClienteController` (API REST para búsqueda).
* [x] **T-17b:** Crear `FacturacionController` (Endpoint para generar factura).
* [x] **T-17c:** Desarrollar Frontend (`index.html`, `style.css`, `app.js`) consumiendo la API.
* [x] **T-18:** Pruebas integrales de flujo (Backend + Frontend).