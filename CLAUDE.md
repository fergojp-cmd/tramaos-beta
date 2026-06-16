# TramaOS — Project OS for Architects

## Contexto del proyecto
Aplicación de gestión de proyectos arquitectónicos. Single-file HTML desplegado en Vercel.
Sin framework, sin build steps. Todo el estado en localStorage.

## Estructura de archivos
```
public/index.html   # Aplicación completa (~402KB) — aquí va todo el código
api/chat.js         # Proxy serverless Node.js para llamadas a Anthropic (evita CORS)
vercel.json         # Configuración de deploy: static + serverless function
```

## Stack
- HTML/CSS/JS vanilla en un solo archivo (`public/index.html`)
- API: el browser llama a `/api/chat` → `api/chat.js` hace el proxy hacia `api.anthropic.com/v1/messages`
- API key en variable de entorno `ANTHROPIC_API_KEY` (en Vercel), no en localStorage
- Desplegado en Vercel (static + Node serverless)
- Sin npm, sin node_modules, sin bundler

## Reglas de desarrollo
- NUNCA dividir en múltiples archivos. Todo el frontend va en `public/index.html`.
- NUNCA añadir npm, build tools ni dependencias externas.
- El estado del proyecto activo se accede con getProject().
- Guardar estado siempre con saveProject() o saveState().
- IDs únicos con uid(). Formateo de moneda con fmt(amount, currency).

## Cómo probar
- Local: abrir `public/index.html` directamente en el browser (doble clic). Las llamadas a `/api/chat` no funcionarán sin Vercel CLI.
- Con API: `vercel dev` para levantar el entorno completo localmente.
