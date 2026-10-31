# BalanceFood — Aplicación web (frontend)

Interfaz web de **BalanceFood**: plataforma para que estudiantes con la Beca de Alimentación JUNAEB comparen precios de platos, registren sus gastos y sepan cuánto pueden gastar cada día para que el saldo les alcance hasta fin de mes.

Proyecto de la asignatura **Computación Web y Móvil** (UTEM) — Tarea 1: Aplicación Web.
Autor: Ian Nicolás Tseng Pereira.

API (backend): https://github.com/tsengian36-rgb/balancefood-backend

## Stack

React 18 · Vite 5 · React Router 6 · JavaScript · CSS simple

## Puesta en marcha

Requisitos: Node 20 o superior y la API corriendo (ver el README del backend).

```bash
npm install
cp .env.example .env     # ajusta VITE_API_URL si la API no está en localhost:3000
npm run dev              # http://localhost:5173
```

Usuario de prueba (creado por el seed de la API): `test@balancefood.cl` / `Password123`

| Script | Qué hace |
|---|---|
| `npm run dev` | Servidor de desarrollo |
| `npm run build` | Build de producción en `dist/` |
| `npm run preview` | Sirve el build localmente |

### Variables de entorno

| Variable | Uso |
|---|---|
| `VITE_API_URL` | URL base de la API, por ejemplo `http://localhost:3000/api/v1`. Se fija al hacer el build. |

## Estructura

```
src/
  api.js            cliente fetch: agrega el JWT y cierra la sesión ante un 401
  auth.jsx          contexto de sesión (login, signup, logout)
  CrudPage.jsx      pantalla CRUD genérica (listar, crear, editar, eliminar)
  App.jsx           navegación y rutas protegidas
  main.jsx          punto de entrada
  index.css         estilos
  pages/
    Login.jsx  Register.jsx  Restaurants.jsx  MenuItems.jsx  Expenses.jsx  Recommendations.jsx
```

## Pantallas y endpoints que consumen

| Pantalla | Endpoints |
|---|---|
| `Login.jsx` | `POST /auth/login` |
| `Register.jsx` | `POST /auth/signup` |
| `App.jsx` (sesión) | `GET /auth/me`, `DELETE /auth/logout` |
| `Restaurants.jsx` | `GET/POST /restaurants`, `PATCH/DELETE /restaurants/:id` |
| `MenuItems.jsx` | `GET/POST /menu_items`, `PATCH/DELETE /menu_items/:id`, `GET /restaurants` |
| `Expenses.jsx` | `GET/POST /expenses`, `PATCH/DELETE /expenses/:id`, `GET /menu_items` |
| `Recommendations.jsx` | `GET /recommendations?budget=` |

## Sesión

El JWT se guarda en `localStorage` y se envía en la cabecera `Authorization: Bearer <token>`. Si la API responde 401 (token vencido o revocado), `api.js` borra el token y la app vuelve a la pantalla de login.

## Despliegue

Sitio estático: `npm ci && npm run build` y publicar `dist/`. Define `VITE_API_URL` con la URL de la API desplegada y agrega una regla de reescritura `/*` → `/index.html` para que React Router funcione al recargar. En la API, `FRONTEND_ORIGIN` debe incluir el dominio del frontend.

## Flujo de trabajo
Ramas `feat/*` → PR a `release` → PR de `release` a `main`. Cada PR contiene un solo cambio con un commit.
Ramas `feat/*` → PR a `release` → PR de `release` a `main`. Cada PR contiene un solo cambio con un commit.
