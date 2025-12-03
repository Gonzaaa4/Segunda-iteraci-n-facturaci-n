# Trabajo Integrador: Sistema de Facturación

Trabajo Integrador para la materia **Programación Orientada a Objetos II**.

## Descripción

Este proyecto es un sistema de gestión y facturación de servicios, su objetivo es automatizar el ciclo comercial de una empresa, permitiendo gestionar clientes (con sus condiciones fiscales de IVA en Argentina), administrar los servicios contratados, generar facturas (individuales y masivas) y registrar los pagos correspondientes.

El proyecto está dividido en dos iteraciones, siguiendo un modelo de Producto Mínimo Viable en la primera entrega.

## ☕ Funcionalidades Principales

* **Gestión de Clientes y Cuentas:** Alta, baja y modificación de clientes y sus cuentas asociadas.
* **Catálogo de Servicios:** Administración de los servicios que ofrece la empresa.
* **Facturación Individual:** Generación de facturas a demanda para una cuenta específica.
* **(Iteración 2) Facturación Masiva:** Generación automática de facturas para todas las cuentas activas.
* **(Iteración 2) Registro de Pagos:** Imputación de pagos totales y parciales.
* **(Iteración 2) Anulación de Facturas:** Capacidad de anular un comprobante emitido.


---

## 🚀 Cómo Correr el Proyecto

Este proyecto es una **aplicación de consola**.

### Requisitos

* Tener instalado Java (JDK 17 o superior).
* Git (para clonar).

### 1. Desde un IDE (Recomendado)

La forma más sencilla de ejecutar el proyecto es importándolo en un IDE:

1.  **Clonar el repositorio:**
    ```bash
    git clone [LA-URL-DE-TU-REPOSITORIO-EN-GITHUB]
    ```
2.  **Abrir con tu IDE:**
    * **IntelliJ IDEA:** `File > Open...` y selecciona la carpeta del proyecto.
    * **VS Code:** `File > Open Folder...` (asegúrate de tener el "Extension Pack for Java").
    * **Eclipse:** `File > Import... > Existing Projects into Workspace`
3.  **Ejecutar:**
    * Localiza el archivo principal (ej. `src/Main.java` o `src/Aplicacion.java`).
    * Haz clic derecho sobre el archivo y selecciona **"Run"**.

### 2. Desde la Terminal (Compilación Manual)

Si prefieres compilar y ejecutar manualmente desde la línea de comandos:

1.  **Clonar el repositorio:**
    ```bash
    git clone [LA-URL-DE-TU-REPOSITORIO-EN-GITHUB]
    cd [NOMBRE-DE-LA-CARPETA-DEL-PROYECTO]
    ```
2.  **Crear un directorio para los compilados (si no existe):**
    ```bash
    mkdir bin
    ```
3.  **Compilar (asumiendo que tu código está en `src/`):**
    ```bash
    # (Desde la raíz del proyecto)
    javac -d bin src/*.java 
    # (Si usas paquetes, ej: src/modelo/*.java, ajusta el comando)
    ```
4.  **Ejecutar el programa:**
    ```bash
    # (Reemplaza "Main" por el nombre de tu clase principal)
    java -cp bin Main
    ```

---

## 📁 Estructura del Proyecto

.
├── docs/                # Contiene toda la documentación
│   ├── erp.md           # Requisitos
│   ├── roadmap.md       # Plan de Iteraciones
│   ├── dp-iteracion-1.md # Diseño Iteración 1
│   └── ...
├── src/                 # Código fuente Java (.java)
│   ├── Main.java        # (O el nombre de tu clase principal)
│   ├── modelo/          # (Clases del dominio: Cliente, Factura, etc.)
│   └── ...
├── bin/                 # Archivos .class (compilados)
└── README.md            # Este archivo

## 👤 Autor

* **GONZALO AQUINO**
