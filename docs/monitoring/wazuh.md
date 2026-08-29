# Monitorización con Wazuh

## Introducción

Wazuh es la plataforma central de seguridad utilizada en SecOps Lab para la monitorización, recopilación de eventos y detección de amenazas en la infraestructura de CoreLab.

## Funciones principales

* **Recopilación y análisis de logs:** Recepción centralizada de registros de sistemas Linux, contenedores Docker y servicios.
* **Detección de intrusiones (HIDS):** Identificación de actividad sospechosa en los host monitorizados.
* **Monitorización de integridad de archivos (FIM):** Control de cambios en ficheros críticos del sistema.
* **Gestión de alertas:** Clasificación y priorización de eventos de seguridad.

## Integración con CoreLab

Wazuh se encarga de observar los componentes activos de CoreLab, proporcionando visibilidad sobre:
* Intentos de inicio de sesión y autenticación.
* Actividad administrativa y de privilegios.
* Cambios en configuraciones de sistema.
* Eventos y comportamiento operativo.

## Configuración y Evidencias

Las configuraciones específicas de agentes y reglas, así como las capturas de pantalla de la interfaz de Wazuh, se documentan en [screenshots/wazuh/](../../screenshots/wazuh/).
