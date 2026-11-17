# Red y conectividad

## Descripción

La comunicación entre los agentes y el servidor Wazuh atraviesa OPNsense, el firewall de CoreLab. Para que los endpoints de otras redes puedan registrar y enviar eventos, se publican los puertos del manager mediante **Destination NAT**.

## Objetivo

Permitir que los agentes ubicados fuera de la VLAN de seguridad (`10.10.20.0/24`) alcancen el manager `10.10.20.2`, manteniendo el tráfico limitado a los puertos estrictamente necesarios.

## Integración en la infraestructura

SecOps Lab utiliza la VLAN de seguridad de CoreLab y se apoya en OPNsense para el filtrado y la traducción de direcciones:

```text
Agentes (WAN / otras VLAN)
            │
            ▼
        OPNsense
   Destination NAT
            │
            ▼
  Wazuh Manager 10.10.20.2
   1514/TCP · 1515/TCP
```

## Configuración

### Reglas NAT para Wazuh

En **Firewall → NAT → Destination NAT** se crearon dos reglas para el servidor `10.10.20.2`:

| Interfaz | Protocolo | Origen | Puerto | Destino | Redirección |
|---|---|---|---|---|---|
| SOC | TCP | WAN | 1514 | Dirección WAN | `10.10.20.2:1514` |
| SOC | TCP | WAN | 1515 | Dirección WAN | `10.10.20.2:1515` |

![Reglas NAT de Wazuh en OPNsense](../screenshots/network/01-nat-wazuh.png)

*Reglas Destination NAT con descripción «Wazuh» para los puertos 1514 y 1515.*

- **1514/TCP** transporta los eventos de los agentes.
- **1515/TCP** se utiliza para el registro de nuevos agentes.

> Tras crear o modificar las reglas hay que pulsar **Aplicar** en OPNsense para que los cambios entren en vigor.

### Puertos requeridos por Wazuh

Según la documentación oficial consultada durante el despliegue, Wazuh utiliza:

| Puerto | Uso |
|---|---|
| 1514/TCP | Comunicación de los agentes con el manager |
| 1515/TCP | Registro de agentes |
| 55000/TCP | API del manager |
| 443/TCP | Dashboard web |

En la captura del laboratorio solo aparecen publicados por NAT los puertos de agentes (1514 y 1515). El dashboard se consume por HTTPS en `https://10.10.20.2` (o `siem.traore.home` en capturas posteriores).

### Acceso a OPNsense

La administración del firewall se realiza por HTTPS en `https://opnsense.traore.home`. El agente de OPNsense se conecta al manager por la red interna, por lo que no depende de las reglas NAT anteriores.

## Verificación

Desde un endpoint Windows se comprobó el puerto del manager:

```powershell
Test-NetConnection 10.10.20.2 -Port 1514
```

Si la conexión no se establece:

1. Verificar que la regla NAT está aplicada.
2. Revisar las reglas de firewall de la interfaz correspondiente.
3. Comprobar que el agente apunta a `10.10.20.2` y no a `0.0.0.0` (ver [resolución de problemas](troubleshooting.md#windows-el-servicio-del-agente-no-arranca)).

## Documentación relacionada

- [Arquitectura de SecOps Lab](architecture.md)
- [Instalación de Wazuh](installation.md)
- [Despliegue de agentes](despliegue-agentes.md)
- [Resolución de problemas](troubleshooting.md)
