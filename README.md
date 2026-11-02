# SecOps Lab

> Laboratorio de operaciones de seguridad sobre CoreLab — monitorización centralizada con Wazuh.

> **Estado:** 🟡 En desarrollo — Fase 1

![Wazuh](https://img.shields.io/badge/Wazuh-005571?style=flat&logo=wazuh&logoColor=white)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=flat&logo=proxmox&logoColor=white)
![OPNsense](https://img.shields.io/badge/OPNsense-D94F00?style=flat&logo=opnsense&logoColor=white)

---

## Descripción

SecOps Lab es el apartado de seguridad de [CoreLab](https://github.com/amtraorek/CoreLab). Su objetivo es monitorizar de forma centralizada la infraestructura (Proxmox, VMs, contenedores, OPNsense y servicios autoalojados), documentando cada decisión técnica y cada paso del despliegue.

---

## Índice

- [Fase 1](#fase-1)
- [Arquitectura](#arquitectura)
- [Componentes](#componentes)
- [Estructura del repositorio](#estructura-del-repositorio)
- [Roadmap](#roadmap)

---

## Fase 1

El objetivo de esta primera versión es tener **Wazuh funcionando**, con **agentes conectados** y un **dashboard** para ver los eventos de CoreLab.

| Paso | Contenido | Estado |
|---|---|---|
| 1 | Desplegar el servidor Wazuh (manager, indexer y dashboard) | 🔄 |
| 2 | Instalar y conectar los agentes en CoreLab | ⏳ |
| 3 | Crear un dashboard con agentes activos y alertas | ⏳ |

---

## Arquitectura

_Pendiente: diagrama del flujo de eventos (agentes → manager → indexer → dashboard)._

Más detalle en [`docs/architecture.md`](docs/architecture.md).

---

## Componentes

| Componente | Función | Estado |
|---|---|---|
| Wazuh manager | Recibe y analiza los eventos | 🔄 |
| Wazuh indexer | Almacena y permite buscar eventos | 🔄 |
| Wazuh dashboard | Visualización de agentes y alertas | 🔄 |
| Agentes Wazuh | Envían eventos desde cada máquina | ⏳ |

---

## Estructura del repositorio

```text
secops-lab/
├── README.md
├── docs/
│   └── architecture.md
├── wazuh/
├── dashboards/
└── screenshots/
    ├── install/
    ├── agents/
    └── dashboard/
```

---

## Roadmap

### Fase 1
- [ ] Servidor Wazuh desplegado
- [ ] Agentes conectados
- [ ] Dashboard propio

---

<div align="center">

**Última actualización:** 03/11/2026

---

### Author

**Amadou Traore Keita**

ASIR Student / SMR Technician · IT Infrastructure · Systems Administration

[![LinkedIn](https://img.shields.io/badge/LinkedIn-amtraorek-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/amtraorek/) [![Email](https://img.shields.io/badge/Email-amtraorek-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:amtraorek@gmail.com)

</div>
