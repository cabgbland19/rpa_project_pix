# Proyecto RPA - Descarga, Almacenamiento y Reporte de Productos

## Descripción del Proyecto
Este proyecto implementa un flujo automatizado de tipo RPA (Robotic Process Automation) que realiza las siguientes acciones:

1. **Consumo de datos desde una API pública.**
2. **Almacenamiento en una base de datos.**
3. **Generación de un reporte Excel.**
4. **Subida del reporte a OneDrive mediante API de Microsoft Graph.**
5. **Carga del reporte en un formulario web con evidencia visual.**

---

## Pasos para Ejecución

### 1. Consumo de API Pública
- Fuente: [Fake Store API](https://fakestoreapi.com)
- Endpoint: https://fakestoreapi.com/products
- Documentación: https://fakestoreapi.com/docs#tag/Products

**Tareas:**
- Solicitud HTTP GET al endpoint.
- Guardar la respuesta como `Productos_YYYY-MM-DD.json`.
- Subir el archivo a OneDrive en la ruta: `/RPA/Logs/Productos_YYYY-MM-DD.json`
- Extraer los siguientes campos: `id`, `title`, `price`, `category`, `description`

### 2. Almacenamiento en Base de Datos
- Se puede usar cualquier motor de base de datos: SQLite, PostgreSQL, SQL Server, etc.
- Tabla: `Productos`

**Estructura de la tabla:**
- `id` (entero, clave primaria)
- `title` (texto)
- `price` (decimal)
- `category` (texto)
- `description` (texto)
- `fecha_insercion` (timestamp)

**Validación:**
- No insertar si el `id` ya existe.

### 3. Generación de Reporte
- Formato: Excel (.xlsx)
- Archivo: `Reporte_YYYY-MM-DD.xlsx`
- Ubicación local: `/Reportes/`
- Subida a OneDrive: `/RPA/Reportes/Reporte_YYYY-MM-DD.xlsx`

**Contenido del Excel:**
- **Hoja 1 - Productos:** todos los productos desde la base de datos.
- **Hoja 2 - Resumen:**
  - Total de productos
  - Precio promedio general
  - Precio promedio por categoría
  - Cantidad de productos por categoría

### 4. Automatización Web - Subida de Formulario
Formulario web en plataforma permitida (Google Forms, Jotform o Typeform).

**Campos requeridos:**
- Nombre del colaborador
- Fecha del reporte
- Comentarios (opcional)
- Subida de archivo (obligatorio)

**Tareas del robot:**
- Acceder al formulario
- Llenar los campos
- Subir el archivo Excel
- Enviar el formulario
- Capturar evidencia visual: `/Evidencias/formulario_confirmacion.png`

---

## Requisitos o Dependencias

### 1. Cuenta Microsoft
Debe contar con una de las siguientes:
- Cuenta de empresa o escuela
- Cuenta de Microsoft Developer (https://developer.microsoft.com/en-us/microsoft-365/dev-program/)

### 2. App Registrada en Azure AD

**Pasos para obtener credenciales:**
- Ingresar a [portal Azure](https://portal.azure.com)
- Crear una aplicación en Azure Active Directory > App Registrations
- Obtener:
  - **Client ID** (ID de la aplicación)
  - **Tenant ID**
  - Crear un **Client Secret** (certificados y secretos > nuevo secreto)
  - Obtener el **User ID** de OneDrive (consultar por API o desde Azure AD)

### 3. Dependencias del Proyecto

#### A. Subida de archivos a OneDrive via Microsoft Graph API
- Esta librería maneja autenticación con Client Credentials Flow (sin interacción de usuario)
- Permite crear carpetas remotas si no existen y subir archivos

#### B. Conversión de JSON a DataTable
- Librería para convertir cadenas JSON a estructuras tabulares para inserción en base de datos

**Nota:**
Estas dos dependencias son privadas y con derechos reservados. Para utilizarlas:
- Contactar al desarrollador para solicitar acceso
- Se entregarán archivos DLL y evidencia de uso autorizado

---

## Enlace del Formulario Usado
> [Formulario de ejemplo - Reporte RPA](https://forms.gle/W6UwYRHmchbtsfvg9) 


