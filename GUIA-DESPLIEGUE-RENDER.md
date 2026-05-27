# 🚀 Guía de Despliegue en Render (Gratis)

## Arquitectura
El backend Express sirve tanto la API como el frontend buildeado de React.
Todo corre en **un solo servicio** → un solo URL.

---

## PASO 1 — Subir el proyecto a GitHub

1. Crea un repositorio en [github.com](https://github.com/new) (puede ser privado)
2. En tu computadora, abre una terminal en la carpeta del proyecto y ejecuta:

```bash
git init
git add .
git commit -m "Primer commit - SWES"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/TU-REPO.git
git push -u origin main
```

---

## PASO 2 — Crear el archivo `backend/.env` con tus datos reales

Crea el archivo `backend/.env` (NO lo subas a GitHub):

```env
PORT=8000
FIREBASE_API_KEY=tu_api_key_real_de_firebase
FRONTEND_VERIFY_URL=https://TU-APP.onrender.com/verify
```

> ⚠️ Este archivo está en `.gitignore`, así que no se sube. Las variables las configuras directamente en Render (ver Paso 4).

---

## PASO 3 — Crear cuenta en Render

1. Ve a [render.com](https://render.com) y regístrate gratis con tu cuenta de GitHub
2. Haz clic en **"New +"** → **"Web Service"**
3. Conecta tu repositorio de GitHub

---

## PASO 4 — Configurar el servicio en Render

Llena estos campos:

| Campo | Valor |
|---|---|
| **Name** | swes-app |
| **Runtime** | Node |
| **Build Command** | `npm run build && cd backend && npm install` |
| **Start Command** | `npm start` |
| **Plan** | Free |

### Variables de entorno (Environment Variables)
Haz clic en **"Add Environment Variable"** y agrega:

| Key | Value |
|---|---|
| `FIREBASE_API_KEY` | tu API key de Firebase |
| `NODE_ENV` | production |

---

## PASO 5 — Variables del Frontend (antes de hacer deploy)

Crea el archivo `frontend/.env` con:

```env
VITE_FIREBASE_API_KEY=tu_api_key
VITE_FIREBASE_AUTH_DOMAIN=tu-proyecto.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=tu-proyecto
VITE_FIREBASE_STORAGE_BUCKET=tu-proyecto.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123:web:abc123
VITE_FIREBASE_MEASUREMENT_ID=G-XXXXXXX
VITE_BACKEND_URL=https://TU-APP.onrender.com/api
```

> ⚠️ Reemplaza `TU-APP` con el nombre que le pusiste en Render.
> Este archivo tampoco se sube a GitHub. Las variables `VITE_*` deben agregarse también en Render como Environment Variables.

---

## PASO 6 — Deploy

1. Haz clic en **"Create Web Service"**
2. Render hará el build automáticamente (tarda ~3-5 minutos la primera vez)
3. Tu app estará en: `https://swes-app.onrender.com`

---

## ⚠️ Nota importante sobre el plan gratuito de Render

El plan gratuito "duerme" el servicio después de 15 minutos de inactividad.
La primera petición después del sueño tarda ~30 segundos en despertar.
Para uso en producción real, considera el plan Starter ($7/mes).

---

## 🔄 Actualizar la app después de cambios

```bash
git add .
git commit -m "descripción del cambio"
git push
```
Render detecta el push y hace redeploy automático.
