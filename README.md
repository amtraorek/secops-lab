# SecOps Lab

> Laboratorio personal de operaciones de seguridad para la monitorización, detección y análisis de la infraestructura CoreLab.

**Estado:** Activo — desarrollo continuo

![Wazuh](https://img.shields.io/badge/Wazuh-4A90E2?style=for-the-badge&logo=wazuh&logoColor=white)
![Suricata](https://img.shields.io/badge/Suricata-EF3B2D?style=for-the-badge&logo=suricata&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=for-the-badge&logo=proxmox&logoColor=white)

---

## Descripción

SecOps Lab es un laboratorio personal de operaciones de seguridad diseñado para monitorizar y analizar la infraestructura de **CoreLab**.

El proyecto funciona como una capa de seguridad sobre la infraestructura existente, recopilando eventos, detectando actividad sospechosa y generando alertas.

La primera versión se centra exclusivamente en la monitorización de CoreLab mediante **Wazuh** y **Suricata**, incorporando **n8n** para la automatización de workflows y **Ollama** para realizar análisis asistido mediante modelos de inteligencia artificial ejecutados localmente.

El objetivo es construir un entorno práctico para aprender y experimentar con monitorización de seguridad, detección de amenazas, análisis de eventos y automatización de respuestas.

---

## Índice

* [Arquitectura](#arquitectura)
* [Infraestructura monitorizada](#infraestructura-monitorizada)
* [Tecnologías](#tecnologías)
* [Monitorización](#monitorización)
* [Detección](#detección)
* [Automatización](#automatización)
* [Análisis mediante IA](#análisis-mediante-ia)
* [Notificaciones](#notificaciones)
* [Pruebas de seguridad](#pruebas-de-seguridad)
* [Investigación de incidentes](#investigación-de-incidentes)
* [Resultados](#resultados)
* [Estructura del repositorio](#estructura-del-repositorio)
* [Roadmap](#roadmap)
* [Consideraciones de seguridad](#consideraciones-de-seguridad)
* [Documentación](#documentación)
* [Autor](#autor)

---

## Arquitectura

La arquitectura de SecOps Lab se integra directamente con CoreLab.

```text
                         CORELAB
                            │
             ┌──────────────┴──────────────┐
             │                             │
          Wazuh                        Suricata
             │                             │
             └──────────────┬──────────────┘
                            │
                       Eventos / Alertas
                            │
                            ▼
                           n8n
                            │
                            ▼
                    Ollama / IA local
                            │
                     Análisis y resumen
                            │
                            ▼
                     Telegram Bot
                            │
                            ▼
                       Notificación
```

El flujo está diseñado para que los eventos de seguridad generados dentro de CoreLab puedan ser detectados, procesados y analizados automáticamente.

La IA se utiliza como herramienta de apoyo al análisis y no como sustituto de la investigación manual.

---

## Infraestructura monitorizada

Actualmente SecOps Lab monitoriza exclusivamente la infraestructura de **CoreLab**.

CoreLab proporciona el entorno sobre el que se generan los eventos que posteriormente son analizados por SecOps Lab.

La infraestructura incluye componentes como:

* Proxmox VE
* Máquinas virtuales
* Contenedores
* Linux
* OPNsense
* Servicios autoalojados
* Servicios de red y almacenamiento

La integración concreta de cada componente se documentará individualmente a medida que sea incorporado al sistema de monitorización.

---

## Tecnologías

| Tecnología       | Función                                                        |
| ---------------- | -------------------------------------------------------------- |
| **Wazuh**        | Monitorización, recopilación de eventos y alertas de seguridad |
| **Suricata**     | Detección de actividad sospechosa en la red                    |
| **n8n**          | Automatización y procesamiento de workflows                    |
| **Ollama**       | Ejecución local de modelos de inteligencia artificial          |
| **Telegram Bot** | Envío de notificaciones de seguridad                           |
| **Linux**        | Sistemas monitorizados y componentes del entorno               |
| **Proxmox VE**   | Infraestructura de virtualización de CoreLab                   |
| **OPNsense**     | Firewall y componente de red de CoreLab                        |
| **Wireshark**    | Análisis manual de tráfico durante investigaciones             |

---

## Monitorización

**Wazuh** constituye uno de los componentes principales de monitorización del proyecto.

Se utiliza para recopilar y analizar eventos procedentes de los sistemas monitorizados y generar alertas cuando se detectan comportamientos relevantes.

Entre los eventos que pueden analizarse se encuentran:

* Intentos de autenticación
* Cambios en sistemas
* Actividad de servicios
* Eventos del sistema
* Comportamientos potencialmente sospechosos
* Alertas de seguridad

La configuración y los procedimientos utilizados se documentan en:

```text
docs/monitoring/
```

---

## Detección

**Suricata** complementa la monitorización de Wazuh proporcionando capacidades de detección sobre el tráfico de red.

El objetivo es identificar actividad potencialmente sospechosa y proporcionar información adicional durante las investigaciones.

Los escenarios de detección se documentarán progresivamente en:

```text
docs/detection/
```

No se consideran implementadas aquellas detecciones que todavía no hayan sido configuradas y verificadas en el entorno.

---

## Automatización

**n8n** se utiliza como plataforma de automatización para conectar los diferentes componentes del laboratorio.

El flujo general es:

```text
Evento
  ↓
Detección
  ↓
n8n
  ↓
Procesamiento
  ↓
Análisis mediante IA
  ↓
Notificación
```

Esto permite reducir tareas repetitivas y crear workflows reproducibles para el tratamiento de alertas.

La automatización no pretende sustituir la investigación manual, sino facilitar el procesamiento inicial de los eventos.

---

## Análisis mediante IA

SecOps Lab incorpora **Ollama** para ejecutar modelos de inteligencia artificial localmente.

La IA se utiliza como herramienta de apoyo para analizar y resumir determinadas alertas de seguridad.

El análisis puede incluir información como:

* Tipo de evento
* Origen de la actividad
* Servicio afectado
* Comportamiento observado
* Nivel de prioridad
* Resumen del evento
* Recomendaciones iniciales para su investigación

Los modelos se ejecutan localmente siempre que sea posible, evitando enviar información de la infraestructura a servicios externos.

La IA no toma decisiones de seguridad de forma autónoma.

---

## Notificaciones

Cuando se detecta un evento relevante, el workflow puede generar una notificación mediante un **bot de Telegram**.

El objetivo es recibir información resumida sin necesidad de acceder constantemente a los dashboards de monitorización.

Un ejemplo conceptual sería:

```text
SECURITY ALERT

Severity: High
Source: Internal host
Service: SSH

Multiple authentication attempts
have been detected.

AI Analysis:
Possible brute-force activity.

Recommended action:
Review the associated events
and investigate the source.
```

Las notificaciones y workflows concretos se documentarán en:

```text
docs/automation/
```

---

## Pruebas de seguridad

SecOps Lab también se utilizará para realizar **pruebas de seguridad controladas contra CoreLab**.

El objetivo es generar escenarios conocidos y comprobar que el sistema es capaz de:

```text
Prueba controlada
       ↓
Actividad generada
       ↓
Detección
       ↓
Alerta
       ↓
Análisis
       ↓
Notificación
       ↓
Investigación
```

Las pruebas se realizarán exclusivamente sobre infraestructura propia y controlada.

Los escenarios y resultados se documentarán en:

```text
docs/security-testing/
```

---

## Investigación de incidentes

Los eventos relevantes podrán documentarse como casos de investigación.

Cada investigación puede incluir:

* Fecha
* Objetivo
* Evento detectado
* Fuente
* Evidencias
* Alertas generadas
* Análisis
* Resultado
* Acciones realizadas

Las evidencias visuales se almacenarán en:

```text
screenshots/incidents/
```

---

## Resultados

El proyecto permitirá documentar resultados reales obtenidos durante la monitorización y las pruebas.

Entre ellos:

* Alertas generadas por Wazuh
* Eventos detectados por Suricata
* Investigaciones de seguridad
* Workflows automatizados
* Análisis realizados mediante IA local
* Notificaciones recibidas mediante Telegram
* Resultados de pruebas controladas

Las evidencias visuales estarán disponibles en:

```text
screenshots/
```

---

## Estructura del repositorio

```text
secops-lab/
├── README.md
├── LICENSE
│
├── docs/
│   ├── architecture/
│   │   └── architecture.md
│   │
│   ├── monitoring/
│   │   └── wazuh.md
│   │
│   ├── detection/
│   │   └── suricata.md
│   │
│   ├── automation/
│   │   └── n8n.md
│   │
│   ├── ai/
│   │   └── ollama.md
│   │
│   ├── incidents/
│   │   └── README.md
│   │
│   └── security-testing/
│       └── README.md
│
└── screenshots/
    ├── architecture/
    ├── wazuh/
    ├── suricata/
    ├── alerts/
    ├── automation/
    └── incidents/
```

La estructura podrá ampliarse a medida que se incorporen nuevas funcionalidades.

---

## Roadmap

### Fase 1 — CoreLab

* [x] Definir arquitectura inicial
* [ ] Integrar Wazuh
* [ ] Integrar Suricata
* [ ] Configurar monitorización
* [ ] Crear detecciones
* [ ] Configurar n8n
* [ ] Integrar Ollama
* [ ] Crear análisis asistido mediante IA
* [ ] Integrar Telegram
* [ ] Realizar pruebas de seguridad controladas
* [ ] Documentar investigaciones

### Fase 2 — Mejora de detección

* [ ] Ampliar las fuentes de eventos
* [ ] Crear nuevas reglas de detección
* [ ] Mejorar los workflows
* [ ] Crear nuevos escenarios de prueba
* [ ] Mejorar la investigación de incidentes

### Futuro

La integración con otros entornos, como un laboratorio de Active Directory y sistemas Windows, se realizará en fases posteriores.

Estas funcionalidades no forman parte del alcance actual de SecOps Lab.

---

## Consideraciones de seguridad

SecOps Lab monitoriza una infraestructura personal y debe mantenerse correctamente aislado.

El proyecto no debe contener:

* Contraseñas
* API keys
* Tokens
* Credenciales
* Secretos de Telegram
* Información privada
* Configuraciones sensibles

Las pruebas de seguridad deben realizarse únicamente contra sistemas propios o entornos sobre los que exista autorización explícita.

---

## Documentación

La documentación detallada del proyecto se encuentra en:

```text
docs/
```

Cada componente dispone de documentación específica sobre sus configuraciones, integración y funcionamiento.

---

<div align="center">

**Última actualización:** 29/08/2026

### Author

**Amadou Traore Keita**

ASIR Student · Cloud · Cybersecurity · Systems Administration

</div>
