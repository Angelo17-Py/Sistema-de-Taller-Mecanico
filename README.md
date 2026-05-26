# SGSI — Sistema de Gestión de Repuestos
## Taller Mecánico · Node.js + Vanilla JS + MySQL

---

## Estructura del proyecto

```
SGSI/
├── database.sql              ← Ejecutar PRIMERO en MySQL
├── package.json
├── .env                      ← Configurar tu DB aquí
├── .gitignore
├── README.md
│
├── backend/
│   ├── server.js             ← Punto de entrada
│   ├── config/
│   │   └── db.js             ← Conexión MySQL (pool)
│   ├── middleware/
│   │   ├── auth.js           ← Verificación JWT
│   │   └── errorHandler.js
│   ├── controladores/
│   │   ├── authControlador.js
│   │   ├── dashboardControlador.js
│   │   ├── repuestosControlador.js
│   │   ├── trabajosControlador.js
│   │   └── usuariosControlador.js
│   └── rutas/
│       ├── auth.js
│       ├── repuestos.js
│       ├── trabajos.js
│       └── usuarios.js
│
└── frontend/
    ├── pages/
    │   ├── login.html
    │   ├── dashboard.html
    │   ├── inventario.html
    │   ├── alertas.html
    │   ├── trabajos.html
    │   ├── historial.html
    │   └── usuarios.html
    ├── js/
    │   ├── api.js            ← Fetch wrapper centralizado
    │   ├── auth.js           ← Manejo de sesión
    │   └── utils.js          ← Helpers (badges, formato, toast)
    ├── css/
    │   └── main.css
    └── components/
        └── sidebar.html      ← Sidebar reutilizable
```

---

## Instalación paso a paso

### Paso 1 — Base de datos MySQL
Abrí MySQL Workbench o la terminal y ejecutá:
```bash
mysql -u root -p < database.sql
```
O en MySQL Workbench: File → Open SQL Script → seleccioná `database.sql` → ejecutá.

### Paso 2 — Configurar el .env
Editá el archivo `.env` y ponés tu contraseña de MySQL:
```env
DB_PASSWORD=tu_contraseña_aqui
```

### Paso 3 — Instalar dependencias y correr el backend
```bash
npm install
npm run dev
# Deberías ver:
# MySQL conectado
# SGSI corriendo en http://localhost:4000
```

### Paso 4 — Abrir el frontend
Usá la extensión **Live Server** de VS Code:
- Click derecho sobre `frontend/pages/login.html`
- "Open with Live Server"
- Se abre en `http://localhost:5500/frontend/pages/login.html`

---

## Usuarios de ejemplo

| Usuario      | Contraseña | Rol           |
|-------------|-----------|---------------|
| carlos.rios  | password  | Administrador |
| juan.perez   | password  | Mecánico      |
| luis.garcia  | password  | Mecánico      |
| pedro.vera   | password  | Mecánico      |

---

## API Endpoints

| Método | Ruta                          | Descripción                 |
|--------|-------------------------------|-----------------------------|
| POST   | /api/auth/login               | Iniciar sesión              |
| GET    | /api/dashboard                | Métricas del panel          |
| GET    | /api/repuestos                | Lista con filtros           |
| GET    | /api/repuestos?alertas=1      | Solo +90 días parados       |
| POST   | /api/repuestos                | Crear (solo Admin)          |
| PUT    | /api/repuestos/:id            | Editar (solo Admin)         |
| PATCH  | /api/repuestos/:id/movimiento | Registrar movimiento        |
| DELETE | /api/repuestos/:id            | Eliminar (solo Admin)       |
| GET    | /api/trabajos                 | Lista con filtro de estado  |
| POST   | /api/trabajos                 | Crear trabajo               |
| PUT    | /api/trabajos/:id             | Editar trabajo              |
| GET    | /api/usuarios                 | Lista (solo Admin)          |
| GET    | /api/usuarios/mecanicos       | Solo mecánicos activos      |
| POST   | /api/usuarios                 | Crear usuario (solo Admin)  |

---

## Errores frecuentes

**ER_ACCESS_DENIED** → Revisá `DB_USER` y `DB_PASSWORD` en `.env`

**ECONNREFUSED** → MySQL no está corriendo. Inicialo primero.

**fetch failed / CORS** → El backend no está corriendo en puerto 4000. Ejecutá `npm run dev`.

**Pantalla en blanco** → Abrí la consola del navegador (F12) y revisá el error.
