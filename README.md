# Gestion_tareas

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build

```
# Gestiónador de Tareas

Este es un proyecto simple para gestionar tareas, donde puedes agregar, editar y eliminar tareas.

## ¿Qué tiene este proyecto?
- **Agregar tareas** con un nombre y estado.
- **Editar tareas** existentes.
- **Eliminar tareas** que ya no necesitas.
- Validaciones para evitar agregar tareas vacías.
- Un diseño básico usando **Vuetify**.

## Requisitos
- Tener **Node.js** instalado (versión 16 o superior).
- Tener **npm** o **yarn** para instalar las dependencias.

## Cómo instalar y usar
1. **Descarga este proyecto** o clónalo desde el repositorio:
   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd gestionador-de-tareas
   ```

2. **Instala las dependencias**:
   ```bash
   npm install
   ```
   O si usas `yarn`:
   ```bash
   yarn install
   ```

3. **Ejecuta la aplicación en modo desarrollo**:
   ```bash
   npm run dev
   ```
   O con `yarn`:
   ```bash
   yarn dev
   ```

4. **Abre la aplicación en tu navegador**: 
   La aplicación estará disponible en el puerto que indique la terminal.

## Estructura del proyecto
- `App.vue`: Componente principal que gestiona las tareas y contiene la tabla.
- `TareaForm.vue`: Componente reutilizable para agregar y editar tareas.
- `main.js`: Punto de entrada donde se inicializa la aplicación.

## Notas importantes
- **Validaciones**: No puedes agregar tareas con campos vacíos.
- **Ediciones**: Al seleccionar una tarea para editar, los datos aparecerán en el formulario.