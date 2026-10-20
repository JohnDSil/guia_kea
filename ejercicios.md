# Ejercicios de Kea DHCP

Resuelve las actividades sin consultar primero `SOLUCIONES.md`.

## Bloque A. Conceptos

1. Describe la función de los cuatro servicios Kea de la tabla del capítulo 1.
2. Explica la diferencia entre una subred DHCP y un pool.
3. ¿Qué diferencia hay entre una reserva y una concesión dinámica?
4. ¿Qué información aporta un registro de nivel `DEBUG` frente a uno de nivel `ERROR`?
5. ¿Por qué una API de control necesita protección adicional?

## Bloque B. Configuración

6. Partiendo del ejemplo de DHCPv4, cambia el pool a `192.168.100.120 - 192.168.100.180`.
7. Cambia el dominio de ejemplo a `laboratorio.test`.
8. Explica por qué `192.168.100.1` debe ser coherente con la topología.
9. Valida la sintaxis del archivo con `jq`.
10. Enumera las comprobaciones que harías antes de aplicar un cambio.

## Bloque C. Reservas y concesiones

11. Propón una reserva para una máquina con MAC `02:00:00:00:00:21` y dirección `192.168.100.21`.
12. Explica qué revisarías si dos máquinas clonadas parecen identificarse del mismo modo.
13. Convierte `1296000` segundos a días.
14. Explica el riesgo de descartar mensajes DHCPRELEASE.

## Bloque D. Seguridad y administración

15. Compara socket Unix, listener HA y Control Agent.
16. Describe un plan para limitar el acceso a la API.
17. Explica qué debes verificar antes de aplicar una recomendación de seguridad encontrada en un manual de otra versión.
18. Justifica el uso de TLS mutuo entre peers cuando la versión y la arquitectura lo admiten.

## Bloque E. Alta disponibilidad y gateway

19. Explica por qué la HA de Kea no garantiza por sí sola la redundancia del gateway.
20. ¿Qué comprueba `sysctl net.ipv4.ip_forward`?
21. Describe los datos necesarios para diagnosticar una regla NAT.
22. ¿Qué papel cumple conntrackd en el laboratorio?
23. Diseña una prueba de conmutación que registre el estado inicial, el fallo y la recuperación.

## Entrega recomendada

Para cada ejercicio práctico, incluye:

- Configuración inicial.
- Cambio realizado.
- Comando de validación.
- Resultado observado.
- Explicación del resultado.
- Riesgos y procedimiento de reversión.
