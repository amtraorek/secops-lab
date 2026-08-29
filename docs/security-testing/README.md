# Pruebas de seguridad

## Descripción

Sección destinada a la planificación y ejecución de pruebas de seguridad controladas sobre la infraestructura de CoreLab.

El objetivo es validar las capacidades de detección del entorno, comprobar el correcto registro de eventos por parte de Wazuh y practicar la investigación de alertas.

## Flujo de trabajo

```text
Prueba
   ↓
Actividad generada
   ↓
Detección
   ↓
Alerta Wazuh
   ↓
Investigación
   ↓
Documentación
```

## Normativa

* Todas las pruebas se realizan exclusivamente sobre infraestructura propia y controlada (CoreLab).
* No se ejecutan pruebas contra sistemas externos ni sin autorización.
* Cada prueba se documenta junto con su resultado y análisis de la alerta generada.
