# Agente Laboral Simon Marin Rojas

Workflows n8n del agente especializado de busqueda laboral para Simon Marin Rojas (Ingeniero Comercial, Analista de Procesos y Automatizacion).

## Arquitectura

| Workflow | ID | Descripcion | Estado |
|---|---|---|---|
| WF-01 | XnyWVCKuFSvWGPqA | Pipeline Postulaciones Automaticas — scraping BNE/GOB/Indeed/CT/Laborum, scoring IA, envio email, registro Notion | Activo |
| WF-01b | bvkZvKfJ8eo3hD0a | Scraping Diario Legacy (GOB+BNE+CT) | Inactivo |
| WF-02 | TLbvtQHwoPTWWy9y | Agente Conversacional Telegram — procesamiento texto/audio/imagen, comandos, memoria | Activo |
| WF-03 | N4o9iXc8PyCf0325 | Registro en Notion — webhook receptor de postulaciones confirmadas | Activo |
| WF-04 | Tf1MIWqHpQ9NKZpa | Email Manual con Aprobacion — generacion IA, preview Telegram, confirmacion, envio SMTP | Activo |
| WF-05 | KAXHj5q99YyM2b2w | Seguimiento Semanal — reporte cada jueves 10:00 AM via Telegram | Activo |
| WF-06 | LoF5nCfl7qEAhwLf | Proxy de Imagen — sirve imagenes de Telegram via webhook | Activo |

## Flujo principal

```
08:30 / 15:00 Chile — WF-01 scraping automatico (5 portales)
09:00 — Resumen matutino Telegram con top ofertas
Telegram /postular_N — WF-02 + WF-04 generan email y piden confirmacion
Confirmacion — WF-04 envia SMTP + WF-03 registra en Notion
Jueves 10:00 — WF-05 reporte semanal de estados
```

## Stack tecnico

- **n8n** self-hosted en VPS
- **Groq API** (llama-3.3-70b-versatile) — generacion de emails y scoring
- **OpenRouter** — modelo vision para imagenes
- **Apify** — scraping Indeed/Computrabajo/Laborum
- **Notion API** — base de datos de postulaciones
- **Telegram Bot** — interfaz de usuario principal
- **Hostinger SMTP** — envio de emails de postulacion

## Modelo IA para emails (WF-04)

Modelo: `llama-3.3-70b-versatile` via Groq API.
Prompt estructurado para generar emails en 3-4 parrafos con logros cuantificables y diferencial tecnico (n8n, Notion ERP, VPS, Apps Script).

## Portales monitoreados

BNE Chile | GetOnBoard | Indeed Chile (Apify) | Computrabajo (Apify) | Laborum (Apify)

---
*Actualizado: 2026-04-06 | Agente configurado: 2026-03-25*
