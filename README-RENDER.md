# Despliegue en Render

## Opción A — Desde el Dashboard (sin YAML)
1. Sube este repositorio a GitHub.
2. En Render: **New > Web Service**.
3. Conecta el repo y selecciona branch (main).
4. **Environment**: Node.
5. **Build Command**: `npm install`
6. **Start Command**: `npm start`
7. **Health Check Path**: `/api/health`
8. **Region**: Oregon (o la que prefieras).
9. **Environment Variables**:
   - `OPENAI_API_KEY` = tu clave
   - `MODEL` = `gpt-5` (o el que definas)
   - `NODE_ENV` = `production`
10. Crear servicio y esperar el build.

> Nota: El plan Free puede dormirse. Para evitarlo, usa Starter/Standard+ o activa autoscaling y min instances.

## Opción B — Blueprint (render.yaml)
1. Asegúrate de tener `render.yaml` en la raíz.
2. En Render: **New > Blueprint** y selecciona tu repo.
3. Ajusta `region`, `plan` (si lo deseas), y crea el servicio.
4. Agrega el Secret `OPENAI_API_KEY` después de crear el servicio (o en el blueprint si usas `sync: false`).

## Verificación
- `GET https://<tu-dominio>.onrender.com/api/health` debe responder `{ ok: true, model: ... }`.
- Generación de bloque: `POST /api/block` (ver README principal).
