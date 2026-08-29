# Automatización con n8n

## Descripción

n8n se utiliza en SecOps Lab como plataforma de automatización de workflows para procesar eventos y alertas de seguridad.

## Flujo de trabajo

1. **Recepción:** Captura de eventos o alertas procedentes de las herramientas de monitorización.
2. **Procesamiento:** Filtrado, estructuración y transformación de los datos.
3. **Análisis:** Envío de información relevante a modelos locales (Ollama) para resumen o análisis asistido.
4. **Notificación:** Envío de resúmenes de alertas a través de un bot de Telegram.

## Configuración y Evidencias

Los workflows, esquemas de automatización y capturas se documentan en [screenshots/automation/](../../screenshots/automation/).
