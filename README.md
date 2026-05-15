# HighSport Frontend

Frontend del sistema de inventario deportivo HighSport. El proyecto esta hecho con HTML, CSS y JavaScript puro, y consume una API REST mediante rutas bajo `/api`.

## Objetivo

Permitir la gestion visual de un inventario deportivo desde el navegador:

- Inicio de sesion y registro de cuenta.
- Panel general con estadisticas del inventario.
- Consulta, busqueda y filtrado de productos.
- Creacion, edicion y eliminacion de productos.
- Gestion de usuarios desde una pantalla administrativa.

## Tecnologias

- HTML5
- CSS3
- JavaScript vanilla
- Google Fonts: `Inter`
- API REST esperada en `/api`

## Estructura

```text
proyecto aula/
├─ index.html
├─ crear-cuenta.html
├─ panel.html
├─ dashboard.html
├─ nuevo-producto.html
├─ editar-producto.html
├─ registro-usuario.html
├─ styles.css
├─ js/
│  ├─ api.js
│  ├─ auth.js
│  └─ productos.js
├─ img/
└─ README.md
```

## Paginas

- `index.html`: pantalla de inicio de sesion.
- `crear-cuenta.html`: formulario para registrar una cuenta nueva.
- `panel.html`: dashboard principal con resumen operativo.
- `dashboard.html`: inventario de productos con tabla, estadisticas y filtros.
- `nuevo-producto.html`: formulario para crear productos.
- `editar-producto.html?id=ID`: formulario para editar o eliminar un producto existente.
- `registro-usuario.html`: administracion de usuarios.

## Archivos JavaScript

### `js/api.js`

Centraliza la comunicacion con el backend.

- Define `API_BASE_URL = "/api"`.
- Ejecuta peticiones HTTP con `fetch`.
- Agrega token de autenticacion desde `localStorage` si existe.
- Muestra alertas visuales con `showAlert`.
- Centraliza redirecciones con `safeRedirect`.

### `js/auth.js`

Maneja autenticacion y proteccion de pantallas.

- Valida si hay sesion activa.
- Guarda token y usuario en `localStorage`.
- Inicia sesion.
- Registra usuarios.
- Cierra sesion.
- Actualiza el avatar con iniciales del usuario.
- Oculta opciones restringidas cuando el usuario no es administrador.

### `js/productos.js`

Contiene la logica del inventario.

- Consulta productos.
- Consulta producto por id.
- Crea productos.
- Actualiza productos.
- Elimina productos.
- Carga la tabla de inventario.
- Calcula estadisticas visibles.
- Filtra productos por nombre y categoria.

## Estilos

El archivo `styles.css` contiene todos los estilos del frontend.

Incluye:

- Variables globales de color.
- Reset basico.
- Pantallas de autenticacion.
- Barra superior y navegacion.
- Panel principal.
- Tarjetas de estadisticas.
- Formularios.
- Tablas.
- Estados visuales de stock.
- Modales y acciones.
- Adaptacion responsive para tablets y celulares.

## Conexion con la API

El frontend espera que el backend responda en la misma direccion del sitio bajo `/api`.

Endpoints usados:

### Usuarios

- `GET /api/usuarios`
- `POST /api/usuarios`
- `PUT /api/usuarios/{id}`
- `DELETE /api/usuarios/{id}`
- `POST /api/usuarios/login`

### Productos

- `GET /api/productos`
- `GET /api/productos/{id}`
- `POST /api/productos`
- `PUT /api/productos/{id}`
- `DELETE /api/productos/{id}`

## Datos esperados

### Producto

```json
{
  "id": 1,
  "nombre": "Nike Air Max 270",
  "precio": 380000,
  "stock": 42,
  "categoria": "Calzado",
  "talla": "M",
  "color": "Rojo"
}
```

### Usuario

```json
{
  "id": 1,
  "nombre": "Kevin Sanchez",
  "email": "kevin@correo.com",
  "rol": "ADMIN"
}
```

### Login

El login espera una respuesta similar a:

```json
{
  "token": "token-generado",
  "usuario": {
    "id": 1,
    "nombre": "Kevin Sanchez",
    "email": "kevin@correo.com",
    "rol": "ADMIN"
  }
}
```

## Como ejecutar

Si el backend sirve estos archivos estaticos, abre la aplicacion desde la URL del servidor, por ejemplo:

```text
http://localhost:8080/index.html
```

Tambien se puede abrir `index.html` directamente en el navegador, pero las llamadas a `/api` solo funcionaran si existe un backend disponible en la misma ruta/base.

## Flujo principal

1. El usuario entra por `index.html`.
2. El formulario llama a `handleLogin`.
3. Si el backend responde correctamente, se guarda la sesion en `localStorage`.
4. El usuario es enviado a `panel.html`.
5. Las paginas privadas ejecutan `protectPage` al cargar.
6. El inventario se consulta desde `dashboard.html` usando `loadProductosTable`.
7. Los formularios de producto usan `handleCreateProducto` y `handleUpdateProducto`.

## Comentarios en el codigo

El codigo del frontend esta comentado por bloques para facilitar la sustentacion y el mantenimiento:

- En HTML se explican secciones, formularios, tablas, modales y scripts embebidos.
- En CSS se explican variables, componentes, layouts y reglas responsive.
- En JavaScript se explican llamadas API, validaciones, manejo de sesion, renderizado y filtros.

## Pruebas sugeridas

1. Abrir `index.html` y probar inicio de sesion.
2. Confirmar que `panel.html` carga estadisticas.
3. Entrar a `dashboard.html` y verificar tabla de productos.
4. Probar busqueda y filtro por categoria.
5. Crear un producto desde `nuevo-producto.html`.
6. Editar un producto desde `editar-producto.html?id=1`.
7. Eliminar un producto desde la tabla o el formulario de edicion.
8. Crear, editar y eliminar usuarios desde `registro-usuario.html`.

## Nota academica

Este frontend esta pensado para explicar claramente la separacion entre interfaz y backend:

- HTML define la estructura de cada pantalla.
- CSS controla la apariencia y adaptacion responsive.
- JavaScript conecta la interfaz con la API REST.
- `localStorage` mantiene datos basicos de sesion en el navegador.
- Los formularios no recargan la pagina; capturan el evento `submit` y llaman funciones JavaScript.
