# simulador-enarm-svc (starter)
Servicio mínimo para generar y evaluar bloques tipo ENARM con un PROMPT MAESTRO.

## Requisitos
- Node.js >= 18
- Variable de entorno `OPENAI_API_KEY`
- Opcional: `MODEL` (por defecto `gpt-5`; alternativas: `gpt-4o`, `gpt-4o-mini`)

## Uso
```bash
npm i
cp .env.example .env   # edita con tu API key
npm run dev
```

### Endpoints
- POST /api/block   -> generador/evaluador/resumen (según `modo`)
- POST /api/health  -> ping

### Ejemplo rápido (curl)
```bash
curl -s http://localhost:3000/api/block   -H "Content-Type: application/json"   -d '{
    "modo":"GENERAR",
    "session_id":"demo-1",
    "usuario_id":"ricky",
    "especialidades_objetivo":["cardiología","ginecología","cirugía"],
    "distribucion_prioridad":{"P1":0.5,"P2":0.3,"P3":0.2},
    "mezcla_dificultad":{"baja":0.3,"intermedia":0.5,"avanzada":0.2},
    "n_casos_por_bloque":3,
    "historial_resumen":"",
    "estadisticas_previas":{}
  }' | jq .publico
```

## Notas
- La API devuelve el JSON completo del modelo. Tu frontend debe mostrar solo `publico`.
- `validatePublicIntegrity` protege contra fugas del tema/respuestas en `modo=GENERAR`.
