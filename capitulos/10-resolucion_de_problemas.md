# Capítulo 10. Resolución de problemas

## Objetivos

- Clasificar fallos de DHCP, control, HA y gateway.
- Aplicar una secuencia de diagnóstico.
- Documentar las causas y las soluciones.

## 1. El servicio no arranca

Comprueba:

1. La sintaxis del archivo.
2. Las opciones incompatibles con la versión.
3. Las interfaces declaradas.
4. Los registros de arranque.
5. Los permisos y recursos necesarios.

No empieces modificando varias opciones a la vez: perderás la capacidad de identificar qué cambio resuelve el problema.

## 2. El cliente no recibe una dirección

Comprueba:

- Que el servidor está activo.
- Que escucha en la interfaz correcta.
- Que el cliente está en la red o VLAN prevista.
- Que el pool tiene direcciones disponibles.
- Que no existe un bloqueo de firewall.
- Que las solicitudes y respuestas aparecen en los registros.

Si el cliente obtiene una IP pero no navega, investiga también el router, las rutas, el forwarding y NAT. No todo problema de conectividad es un problema de DHCP.

## 3. La reserva no se aplica

Revisa la identidad del cliente, la dirección reservada, el contexto en el que se ha declarado la reserva y las opciones relacionadas con Client ID y MAC.

En máquinas virtuales clonadas, comprueba si se repiten identificadores. El material señala `match-client-id: false` como parte de su escenario, pero no debe copiarse sin entender la identidad de los clientes.

## 4. El Control Agent no responde

Comprueba:

- Que el servicio está instalado y activo.
- La dirección y el puerto de escucha.
- La conectividad desde el equipo administrador.
- El firewall.
- La configuración del canal de control.
- Los requisitos de TLS y autenticación.
- La compatibilidad de la configuración con la versión.

No abras el puerto a toda la red como solución rápida.

## 5. Los peers HA no se comunican

Revisa:

- Direcciones y puerto configurados.
- Reglas de firewall.
- `this-server-name`.
- Módulo HA.
- Listener de control.
- Certificados y autenticación mutua cuando se utilizan.
- Sincronización horaria.

El material cita el puerto `8000` como parte de su laboratorio; verifica el puerto real de tu instalación.

## 6. La VIP o el gateway no funciona

Comprueba:

- Interfaces internas y externas.
- Direcciones IP.
- Reenvío IPv4.
- Ruta por defecto.
- Reglas nftables.
- Configuración Keepalived/VRRP.
- Anuncios de la VIP.
- Estado y direcciones de sincronización de conntrackd.

Si DHCP funciona pero no hay salida a otras redes, empieza por comprobar la ruta y las reglas de forwarding.

## 7. Método de diagnóstico

Sigue siempre esta secuencia:

1. Describe el síntoma observable.
2. Define el resultado esperado.
3. Identifica la capa afectada.
4. Reúne registros y estado actual.
5. Formula una hipótesis comprobable.
6. Cambia una sola variable.
7. Repite la prueba.
8. Documenta el resultado.
9. Prepara la reversión si el cambio no funciona.

## Ejercicio final

Un cliente obtiene una IP válida, pero no alcanza una red externa. El servidor Kea aparece activo.

Prepara un diagnóstico que examine, en este orden, las opciones entregadas por DHCP, la configuración del cliente, la ruta por defecto, el reenvío IPv4, el firewall y NAT. Explica qué evidencia buscarías en cada paso.

## Checklist

- [ ] He identificado la capa afectada.
- [ ] He reunido evidencias antes de cambiar la configuración.
- [ ] He probado una hipótesis cada vez.
- [ ] He verificado el resultado después del cambio.
- [ ] He documentado la solución y la forma de revertirla.
