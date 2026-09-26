# SecOps Lab

> Laboratorio personal de operaciones de seguridad para la monitorización, detección y análisis de la infraestructura CoreLab.

**Estado:** Activo — desarrollo continuo

![Wazuh](https://img.shields.io/badge/Wazuh-4A90E2?style=for-the-badge&logo=wazuh&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=for-the-badge&logo=proxmox&logoColor=white)

---

## Descripción

SecOps Lab es un laboratorio personal de operaciones de seguridad diseñado para monitorizar y analizar la infraestructura de **CoreLab**.

El proyecto funciona como una capa de seguridad sobre la infraestructura existente, recopilando eventos y generando alertas.

La primera versión se centra exclusivamente en la monitorización de CoreLab mediante **Wazuh**. Otros componentes (detección de red, automatización de workflows, análisis asistido mediante IA local, notificaciones) se irán incorporando en fases futuras a medida que estén implementados y verificados.

El objetivo es construir un entorno práctico para aprender y experimentar con monitorización de seguridad, detección de amenazas, análisis de eventos y automatización de respuestas.

---

## Índice

* [Arquitectura](#arquitectura)
* [Infraestructura monitorizada](#infraestructura-monitorizada)
* [Tecnologías](#tecnologías)
* [Monitorización](#monitorización)
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
                          Wazuh
                            │
                       Eventos / Alertas
```

Este flujo se ampliará progresivamente a medida que se incorporen nuevos componentes (ver Roadmap).

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
| **Linux**        | Sistemas monitorizados y componentes del entorno               |
| **Proxmox VE**   | Infraestructura de virtualización de CoreLab                   |
| **OPNsense**     | Firewall y componente de red de CoreLab                        |

---

## Monitorización

**Wazuh** constituye el componente principal de monitorización del proyecto.

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

El proyecto permitirá documentar resultados reales obtenidos durante la monitorización.

Entre ellos:

* Alertas generadas por Wazuh
* Investigaciones de seguridad
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
├── wazuh/
│   └── rules/
│
├── docs/
│   ├── architecture/
│   │   └── architecture.md
│   │
│   ├── monitoring/
│   │   └── wazuh.md
│   │
│   ├── incidents/
│   │   └── README.md
│   │
│   └── security-testing/
│       └── README.md
│
├── dashboards/
│   ├── grafana/
│   └── wazuh/
│
└── screenshots/
    ├── architecture/
    ├── wazuh/
    ├── alerts/
    └── incidents/
```

La estructura podrá ampliarse a medida que se incorporen nuevas funcionalidades.

---

## Roadmap

### Fase 1 — CoreLab (en curso)

* [x] Definir arquitectura inicial
* [x] Integrar Wazuh
* [ ] Configurar monitorización avanzada
* [ ] Realizar pruebas de seguridad controladas
* [ ] Documentar investigaciones

### Fase 2 — Ampliación

* [ ] Integrar Suricata (detección de red)
* [ ] Configurar n8n (automatización de workflows)
* [ ] Integrar Ollama (análisis asistido mediante IA local)
* [ ] Integrar Telegram (notificaciones)
* [ ] Ampliar fuentes de eventos y reglas de detección

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

**Última actualización:** 26/09/2026

---
### Author

**Amadou Traore Keita**

ASIR Student · Cloud · Cybersecurity · Systems Administration

[![LinkedIn](https://img.shields.io/badge/LinkedIn-amtraorek-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/amtraorek/) [![Email](https://img.shields.io/badge/Email-amtraorek-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:amtraorek@gmail.com)

</div>