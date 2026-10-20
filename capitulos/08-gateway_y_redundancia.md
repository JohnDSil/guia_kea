# Capítulo 8. Gateway y redundancia de red

## Objetivos

- Diferenciar la HA de Kea de la redundancia del gateway.
- Comprender el papel de VRRP, conntrackd y nftables.
- Identificar los fallos habituales de encaminamiento y NAT.

## 1. Arquitectura del laboratorio

El material combina varios componentes:

- Dos nodos Kea.
- Keepalived/VRRP para gestionar una dirección IP virtual (VIP) de gateway.
- conntrackd para sincronizar estado de conexiones.
- nftables para filtrado, encaminamiento y traducción de direcciones.
- Una interfaz interna y otra externa por nodo.

La alta disponibilidad DHCP y la alta disponibilidad del gateway son funciones distintas. Que Kea funcione correctamente no garantiza que el encaminamiento sobreviva a la caída del gateway, ni a la inversa.

## 2. Encaminamiento

Comprueba que el sistema tiene habilitado el reenvío IPv4 cuando actúa como router:

```bash
sysctl net.ipv4.ip_forward
```

El resultado esperado en un gateway que debe reenviar IPv4 es `1`.

Para una inspección inicial de rutas:

```bash
ip route
ip address
```

Verifica que la ruta por defecto utiliza la interfaz externa prevista y que las reglas de reenvío corresponden al sentido real del tráfico.

El material destaca errores como confundir la dirección del tráfico entre las interfaces interna y externa o no disponer de una ruta por defecto adecuada.

## 3. NAT y nftables

El material diferencia entre `masquerade` y `SNAT` a una dirección de origen concreta. La elección depende de cómo estén configuradas las direcciones externas y la VIP.

No copies una regla NAT sin confirmar:

- Interfaz de entrada.
- Interfaz de salida.
- Subred de origen.
- Dirección de traducción prevista.
- Reglas de forwarding.
- Política de firewall.

Ambas máquinas deben tener reglas coherentes con el diseño de conmutación.

## 4. Keepalived/VRRP

Revisa:

- Dirección de la VIP.
- Interfaces asociadas.
- Prioridades de los nodos.
- Grupo de sincronización cuando el diseño lo requiera.
- Comportamiento de la VIP durante la conmutación.

El material señala que una VIP externa puede requerir un tratamiento específico de anuncios de dirección, incluida la configuración de `Address Ignore` según el diseño.

## 5. conntrackd

conntrackd se utiliza en el laboratorio para sincronizar el estado de seguimiento de conexiones. Si el objetivo es conservar sesiones TCP durante la conmutación, hay que comprobar las direcciones de sincronización, la configuración del demonio y las reglas asociadas.

El material menciona la necesidad de revisar la configuración de conntrackd y el uso de su comprobación con `conntrackd -c`. Consulta el manual local antes de utilizar opciones de configuración o recuperación en producción.

## Ejercicios

1. ¿Qué diferencia hay entre la VIP del gateway y la dirección real de cada nodo?
2. ¿Qué comprueba `net.ipv4.ip_forward`?
3. ¿Qué datos necesitas antes de elegir entre `masquerade` y `SNAT`?
4. ¿Por qué sincronizar el estado de conexiones puede ayudar a conservar sesiones TCP?
5. Explica por qué la HA de Kea no sustituye a la HA del gateway.

## Checklist

- [ ] Las interfaces interna y externa están identificadas.
- [ ] El reenvío IPv4 está habilitado cuando se necesita.
- [ ] La ruta por defecto es correcta.
- [ ] Las reglas nftables corresponden al sentido del tráfico.
- [ ] La VIP se anuncia en las condiciones previstas.
- [ ] conntrackd tiene direcciones y configuración coherentes.
- [ ] Se han definido pruebas de conmutación.
