# Detección con Suricata

## Descripción

Suricata se integra en SecOps Lab para proporcionar capacidades de detección de amenazas e intrusiones a nivel de red, complementando la monitorización de sistemas proporcionada por Wazuh.

## Funciones principales

* Inspección profunda de paquetes (DPI).
* Detección de patrones y firmas de ataques.
* Monitorización de tráfico de red.
* Generación de alertas ante actividad sospechosa o anómala.

## Integración

Suricata monitoriza el tráfico de la infraestructura de CoreLab, registrando eventos que posteriormente pueden ser correlacionados, procesados mediante automatizaciones (n8n) y analizados.

## Configuración y Evidencias

Las reglas, configuraciones y capturas relacionadas se documentan en [screenshots/suricata/](../../screenshots/suricata/).
