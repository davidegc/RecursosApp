# Recursos App - Google Apps Script

Aplicación web simple creada con Google Apps Script para gestionar una colección de recursos (enlaces, herramientas, documentos, etc.) almacenados en una Hoja de Cálculo de Google (Google Sheet). Permite visualizar, añadir, editar, marcar como favoritos y gestionar categorías y tipos de recursos.

## Características

* **Visualización de Recursos:** Muestra los recursos agrupados por categoría en tarjetas interactivas.
* **Búsqueda:** Filtra recursos por nombre, descripción, tipo, autor, etc.
* **Añadir/Editar Recursos:** Formulario modal para crear nuevos recursos o modificar existentes.
* **Gestión de Categorías:** Añade y edita categorías directamente desde la interfaz.
* **Gestión de Tipos:** Lee los tipos de recurso desde una hoja dedicada en Google Sheets.
* **Favoritos:** Marca/desmarca recursos como favoritos.
* **Estado:** Marca recursos como Activos o Inactivos.
* **Contador de Clics:** Registra cuántas veces se ha abierto la URL de un recurso.
* **Diseño Responsivo:** Interfaz adaptable a diferentes tamaños de pantalla con menú lateral desplegable en móviles.
* **Embebible:** Diseñada para ser insertada en un sitio de Google Sites.

## Prerrequisitos

1.  **Cuenta de Google:** Necesaria para crear/usar Google Sheets y Apps Script.
2.  **Google Sheet:** Una hoja de cálculo configurada con las siguientes pestañas (hojas):
    * **`Recursos`**: Debe contener las columnas definidas en `Code.gs` (ID, Nombre, Descripcion, URL, Categoria, Tipo, Estatus, Autor, Recursos Adicionales, Favorito, Clicks). El script **no** crea esta hoja.
    * **`Categorias`**: El script la creará automáticamente si no existe, con la columna `NombreCategoria`.
    * **`Tipos`**: Debe ser creada manualmente con la columna `NombreTipo` en A1. A partir de A2, lista los tipos de recurso válidos (ej. "Enlace", "Herramienta Web", "Software").

## Configuración

1.  **ID de la Hoja de Cálculo:**
    * Abre tu Google Sheet.
    * Copia el ID largo de la URL (la cadena entre `/d/` y `/edit`).
    * Abre el archivo `Code.gs` en el editor de Apps Script.
    * Reemplaza `'TU_SHEET_ID_AQUI'` (o el ID actual) en la constante `SHEET_ID` con el ID que copiaste.
2.  **Nombres de las Hojas:**
    * Verifica que las constantes `RESOURCE_SHEET_NAME`, `CATEGORY_SHEET_NAME`, y `TYPE_SHEET_NAME` en `Code.gs` coincidan **exactamente** (mayúsculas/minúsculas) con los nombres de las pestañas en tu Google Sheet (`Recursos`, `Categorias`, `Tipos`).
3.  **Hoja "Tipos":**
    * Crea la hoja llamada `Tipos`.
    * En A1 escribe `NombreTipo`.
    * En A2, A3, etc., escribe los tipos de recurso que deseas usar.

## Instalación y Despliegue

Puedes configurar el proyecto usando el editor web de Apps Script o localmente con `clasp`.

**Opción 1: Usando el Editor Web (Manual)**

1.  Crea un nuevo proyecto de Apps Script vinculado a tu Google Sheet (Herramientas > Editor de secuencia de comandos) o independiente (script.google.com).
2.  Copia el contenido de `Code.gs` y pégalo en el archivo `Código.gs` del editor.
3.  Crea nuevos archivos HTML para `Index.html`, `JavaScript.html` y `Stylesheets.html` (Archivo > Nuevo > Archivo HTML).
4.  Copia y pega el contenido correspondiente de los archivos locales en los archivos HTML creados en el editor.
5.  **Configura el `SHEET_ID`** en `Code.gs`.
6.  Guarda todos los archivos.
7.  Ve a "Implementar" > "Nueva implementación".
8.  Haz clic en el icono de engranaje ("Seleccionar tipo") y elige "Aplicación web".
9.  Configura la implementación:
    * **Descripción:** (Opcional) Ej. "Versión inicial Recursos App".
    * **Ejecutar como:** "Yo".
    * **Quién tiene acceso:** "Cualquier usuario" o "Cualquier usuario con cuenta de Google".
10. Haz clic en "Implementar".
11. **Autoriza los permisos** que solicite el script (acceso a Sheets, etc.).
12. Copia la **URL de la aplicación web** (`/exec`) proporcionada. Esta es la URL para acceder a tu aplicación.

**Opción 2: Usando `clasp` (Recomendado para desarrollo continuo)**

1.  Instala Node.js y npm si no los tienes.
2.  Instala `clasp` globalmente: `npm install -g @google/clasp`
3.  Autentícate con Google: `clasp login`
4.  Crea un nuevo proyecto de Apps Script (o usa uno existente) y copia su Script ID desde "Configuración del proyecto" (icono de engranaje).
5.  Clona el proyecto en una carpeta local: `clasp clone "<Script ID>"` (reemplaza `<Script ID>`). O si ya tienes los archivos localmente, crea un archivo `.clasp.json` con `{"scriptId":"<Script ID>"}`.
6.  Copia los archivos `Code.gs`, `Index.html`, `JavaScript.html`, `Stylesheets.html` (y `appsscript.json` si existe) a la carpeta del proyecto local.
7.  **Configura el `SHEET_ID`** en `Code.gs`.
8.  Sube los archivos al proyecto de Apps Script: `clasp push`
9.  Abre el proyecto en el editor web de Apps Script (`clasp open`).
10. Sigue los pasos 7-12 de la Opción 1 (Manual) para crear o actualizar la implementación web.

## Embeber en Google Sites

1.  Asegúrate de haber desplegado la aplicación web y de que la función `doGet` en `Code.gs` incluya `.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)`.
2.  Copia la URL de la aplicación web (`/exec`).
3.  Edita tu Google Site.
4.  Ve a "Insertar" > "Insertar URL".
5.  Pega la URL `/exec`.
6.  Ajusta el tamaño del widget insertado.

## Archivos del Proyecto

* `Code.gs`: Lógica del lado del servidor (Apps Script) para interactuar con Google Sheets.
* `Index.html`: Estructura HTML principal de la aplicación web.
* `JavaScript.html`: Código JavaScript del lado del cliente para interactividad, llamadas al servidor y manipulación del DOM.
* `Stylesheets.html`: Estilos CSS (usando Tailwind CSS vía CDN y estilos personalizados) para la apariencia visual.
* `appsscript.json`: Manifiesto del proyecto (define permisos, etc.).

