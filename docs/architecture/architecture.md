# Arquitectura de SecOps Lab

## Descripción general

SecOps Lab actúa como la capa de seguridad y monitorización de **CoreLab**. Su diseño está enfocado en proporcionar visibilidad sobre la infraestructura mediante la recopilación, análisis y detección de eventos de seguridad.

## Diagrama de Arquitectura

```text
                 CoreLab
                    │
                    ▼
             Security Events
                    │
                    ▼
                  Wazuh
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
      Alerts              Analysis
          │                   │
          └─────────┬─────────┘
                    ▼
            Security Testing
```

## Componentes

1. **CoreLab (Infraestructura monitorizada):**
   - Proxmox VE (virtualización)
   - OPNsense (firewall y router)
   - Sistemas Linux y contenedores Docker

2. **Wazuh (Plataforma de seguridad):**
   - Recopilación de logs y eventos del sistema.
   - Monitorización de integridad de archivos (FIM).
   - Generación de alertas basadas en reglas.

3. **Pruebas de seguridad e investigación:**
   - Ejecución controlada de pruebas sobre CoreLab.
   - Análisis y documentación de alertas e incidentes simulados.
