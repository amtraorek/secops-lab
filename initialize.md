# SecOps Lab

🇪🇸 [Español](#-español) · 🇬🇧 [English](#-english)

---

# 🇪🇸 Español

Laboratorio de operaciones de seguridad (SecOps) que monitoriza la infraestructura del homelab **CoreLab** (Proxmox, VMs, contenedores LXC, OPNsense y servicios autoalojados). El objetivo es construir, paso a paso y documentando cada decisión, un flujo realista de detección, alerta y respuesta.

> **Estado:** Fase 1 en curso · Última actualización del roadmap: 26/10/2026

## Stack

| Herramienta | Uso | Fase |
|---|---|---|
| Wazuh | Monitorización y gestión de eventos (SIEM/XDR) | 1 |
| Suricata | Detección de intrusiones en red (IDS) | 2 |
| n8n | Automatización de workflows | 2 |
| Ollama | IA local para analizar y resumir alertas | 2 |
| Telegram Bot | Notificaciones al móvil | 2 |

## Arquitectura (versión 1)

```
                +--------------------------+
                |   VM Wazuh Server        |
                |  manager+indexer+dash    |
                +------------^-------------+
                             |
     +-----------+-----------+-----------+-------------+
     |           |           |           |             |
 Agentes LXC  Agentes VM  Agente Host   OPNsense     Servicios
 (importantes)  (Linux)    Proxmox      (syslog)    autoalojados
```

- **Servidor Wazuh:** una única VM dedicada en Proxmox (all-in-one: manager, indexer y dashboard).
- **Agentes:** uno por cada VM, cada LXC relevante y el host Proxmox. En hosts con Docker, un solo agente en el host con el módulo de Docker activado.
- **OPNsense:** no admite agente; envía sus logs por syslog al servidor.
- **Agentes con nombres claros y agrupados** por función (`proxy`, `bases-de-datos`, `apps`...).

## Roadmap

### Fase 1: CoreLab (en curso)
Primera versión centrada solo en Wazuh monitorizando CoreLab.

- [ ] Inventario de CoreLab y diagrama de arquitectura
- [ ] Instalación del servidor Wazuh (VM dedicada)
- [ ] Primer agente en una VM Linux sencilla (validación)
- [ ] Agentes en LXC clave, VMs y host Proxmox
- [ ] Logs de OPNsense por syslog
- [ ] Revisión de módulos: FIM, detección de vulnerabilidades y SCA
- [ ] Pruebas de seguridad controladas (fuerza bruta SSH, cambio en fichero vigilado, escaneo con nmap)
- [ ] Documentación de investigaciones, con capturas

### Fase 2: Detección de red y automatización
- [ ] Suricata (empezar en modo IDS, no IPS) con reglas ET Open y alertas hacia Wazuh
- [ ] Telegram Bot con alertas de nivel alto
- [ ] n8n conectado a Wazuh por webhook (enriquecimiento y filtrado de alertas)
- [ ] Ollama para resumir alertas y sugerir qué revisar primero
- [ ] Más fuentes de logs y reglas propias en `local_rules.xml`

### Ideas futuras
- **v3:** Active Response ajustada, enriquecimiento con AbuseIPDB/VirusTotal/OTX, playbooks y gestión de casos
- **v4:** auditd/Sysmon, logs centralizados, métricas (Prometheus + Grafana / Uptime Kuma), honeypot interno
- **v5:** red team controlado, mapeo a MITRE ATT&CK, Atomic Red Team, purple team
- **v6:** integración con la honeynet de Azure (CloudTrap) y lab de Active Directory / Windows *(fuera del alcance actual)*
- **Transversal:** hardening (CIS), copias de seguridad y restauración, Ansible para desplegar agentes

## Estructura del repositorio

```
secops-lab/
├── wazuh/          # Configuración del servidor y de los agentes
├── dashboards/     # Dashboards exportados
├── incidents/      # Registro de incidentes y pruebas
├── docs/
│   ├── architecture/
│   ├── monitoring/
│   ├── detection/
│   ├── automation/
│   ├── ai/
│   ├── incidents/
│   └── security-testing/
└── screenshots/    # Capturas organizadas por categoría
```

## Buenas prácticas del laboratorio

- Sincronización horaria (NTP) en todas las máquinas
- Cambiar contraseñas por defecto y no exponer el dashboard de Wazuh a internet
- Snapshot de la VM de Wazuh antes de cada actualización
- Controlar el espacio en disco del indexer y definir la retención de logs
- Lista blanca propia antes de activar Active Response

## Documentación

Cada paso, decisión y prueba se documenta en `docs/` con capturas en `screenshots/`.

> Este repositorio es un laboratorio personal con fines de aprendizaje. Todas las pruebas se realizan en un entorno propio y controlado.

---

# 🇬🇧 English

Security operations (SecOps) lab that monitors my **CoreLab** homelab infrastructure (Proxmox, VMs, LXC containers, OPNsense and self-hosted services). The goal is to build, step by step and documenting every decision, a realistic detection, alerting and response workflow.

> **Status:** Phase 1 in progress · Roadmap last updated: 2026-10-26

## Stack

| Tool | Purpose | Phase |
|---|---|---|
| Wazuh | Monitoring and event management (SIEM/XDR) | 1 |
| Suricata | Network intrusion detection (IDS) | 2 |
| n8n | Workflow automation | 2 |
| Ollama | Local AI to analyze and summarize alerts | 2 |
| Telegram Bot | Mobile notifications | 2 |

## Architecture (version 1)

- **Wazuh server:** a single dedicated VM on Proxmox (all-in-one: manager, indexer and dashboard).
- **Agents:** one per VM, per relevant LXC and on the Proxmox host. On Docker hosts, a single agent on the host with the Docker module enabled.
- **OPNsense:** no agent support; logs are sent to the server via syslog.
- **Clear agent names and groups** by role (`proxy`, `databases`, `apps`...).

## Roadmap

### Phase 1: CoreLab (in progress)
First version focused only on Wazuh monitoring CoreLab.

- [ ] CoreLab inventory and architecture diagram
- [ ] Wazuh server installation (dedicated VM)
- [ ] First agent on a simple Linux VM (validation)
- [ ] Agents on key LXCs, VMs and the Proxmox host
- [ ] OPNsense logs via syslog
- [ ] Review of modules: FIM, vulnerability detection and SCA
- [ ] Controlled security tests (SSH brute force, watched-file change, nmap scan)
- [ ] Documented investigations with screenshots

### Phase 2: Network detection and automation
- [ ] Suricata (start in IDS mode, not IPS) with ET Open rules and alerts forwarded to Wazuh
- [ ] Telegram Bot for high-severity alerts
- [ ] n8n connected to Wazuh via webhook (alert enrichment and filtering)
- [ ] Ollama to summarize alerts and suggest what to check first
- [ ] More log sources and custom rules in `local_rules.xml`

### Future ideas
- **v3:** tuned Active Response, enrichment with AbuseIPDB/VirusTotal/OTX, playbooks and case management
- **v4:** auditd/Sysmon, centralized logs, metrics (Prometheus + Grafana / Uptime Kuma), internal honeypot
- **v5:** controlled red team, MITRE ATT&CK mapping, Atomic Red Team, purple team
- **v6:** integration with the Azure honeynet (CloudTrap) and Active Directory / Windows lab *(out of current scope)*
- **Cross-cutting:** hardening (CIS), backup and restore testing, Ansible to deploy agents

## Repository structure

```
secops-lab/
├── wazuh/          # Server and agent configuration
├── dashboards/     # Exported dashboards
├── incidents/      # Incident and test records
├── docs/
│   ├── architecture/
│   ├── monitoring/
│   ├── detection/
│   ├── automation/
│   ├── ai/
│   ├── incidents/
│   └── security-testing/
└── screenshots/    # Screenshots organized by category
```

## Lab best practices

- Time synchronization (NTP) on all machines
- Change default passwords and never expose the Wazuh dashboard to the internet
- Snapshot the Wazuh VM before every upgrade
- Monitor indexer disk usage and define log retention
- Set up your own allowlist before enabling Active Response

## Documentation

Every step, decision and test is documented in `docs/` with screenshots in `screenshots/`.

> This repository is a personal learning lab. All tests are performed in my own controlled environment.
