# Arquitectura de SecOps Lab

## Descripción general

SecOps Lab actúa como la capa de seguridad y monitorización de **CoreLab**. Su diseño está enfocado en proporcionar visibilidad sobre la infraestructura mediante la recopilación, análisis y detección de eventos de seguridad.

El laboratorio se apoya en **Wazuh** como plataforma central de monitorización, complementada por dashboards y evidencias de despliegue, agentes y alertas.

## Diagrama de arquitectura

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

1. **CoreLab (infraestructura monitorizada):**
   - Proxmox VE (virtualización).
   - OPNsense (firewall y router).
   - Sistemas Linux y contenedores Docker.

2. **Wazuh (plataforma de seguridad):**
   - Recopilación de logs y eventos del sistema.
   - Monitorización de integridad de archivos (FIM).
   - Generación de alertas basadas en reglas.
   - Gestión centralizada de agentes.

3. **Dashboards:**
   - Visualización de alertas, eventos y estado de los agentes.
   - Paneles específicos de Wazuh y Grafana.

4. **Pruebas de seguridad e investigación:**
   - Ejecución controlada de pruebas sobre CoreLab.
   - Análisis y documentación de alertas e incidentes simulados.

## Despliegue y evidencias

La documentación visual del laboratorio se organiza de la siguiente forma:

```text
screenshots/
├── install/     # Instalación y puesta en marcha de Wazuh
├── agents/      # Registro y estado de los agentes
└── dashboard/   # Alertas, eventos y paneles de visualización
```

Las reglas personalizadas se almacenan en [`wazuh/rules/`](../wazuh/rules/) y los dashboards en [`dashboards/`](../dashboards/).

## Alcance actual

La primera versión se centra en la monitorización de CoreLab mediante Wazuh. Componentes adicionales como detección de red, automatización de workflows, análisis asistido mediante IA local y notificaciones se incorporarán en fases posteriores, una vez implementados y verificados.
