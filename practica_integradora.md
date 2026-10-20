# Práctica integradora: Kea, seguridad y redundancia

## Objetivo

Construir y documentar un laboratorio de DHCPv4 con reservas, almacenamiento, registros y una planificación de administración segura. Como ampliación, diseñar la alta disponibilidad de Kea y la redundancia del gateway.

## Fase 1. Diseño

Antes de instalar, documenta:

- Sistema operativo y versión.
- Versión de Kea.
- Nombre de la interfaz interna.
- Subred de laboratorio.
- Dirección del gateway.
- Rango dinámico.
- Direcciones reservadas.
- DNS que se entregará a los clientes.

Usa una red aislada y comprueba que no se solapa con otra red activa.

## Fase 2. DHCPv4 básico

1. Configura la interfaz interna.
2. Define una subred.
3. Define un pool.
4. Configura las opciones de router y DNS.
5. Valida el archivo.
6. Arranca o recarga el servicio siguiendo el procedimiento de tu sistema.
7. Comprueba el estado y los registros.

**Evidencias:** archivo de configuración sin secretos, salida de validación, estado del servicio y concesión recibida por un cliente.

## Fase 3. Reservas

1. Añade una reserva de prueba.
2. Verifica la identidad del cliente.
3. Renueva la concesión de forma controlada.
4. Comprueba la dirección recibida.
5. Confirma los eventos en los registros.

Documenta cualquier diferencia entre el comportamiento observado y el esperado.

## Fase 4. Leases y registros

1. Identifica el backend configurado.
2. Localiza el archivo o sistema de almacenamiento.
3. Identifica los eventos de inicio y asignación.
4. Documenta cómo comprobarías una liberación y una expiración.

No elimines manualmente los archivos de leases mientras el servicio los está utilizando.

## Fase 5. Administración segura

1. Identifica los canales de control disponibles.
2. Comprueba la versión y su documentación.
3. Define qué equipos pueden administrar el servicio.
4. Restringe los puertos de control.
5. Documenta el mecanismo de cifrado y autenticación aplicable.

No expongas la interfaz de control a Internet ni compartas claves privadas o contraseñas en el repositorio.

## Fase 6. Diseño de HA

Si dispones de dos nodos, documenta:

- Nombre de cada nodo.
- Direcciones y puertos de comunicación.
- Módulo y configuración HA.
- Protección del canal.
- Estado esperado de ambos peers.
- Procedimiento de conmutación y recuperación.

Primero valida la comunicación normal; después ejecuta pruebas de fallo en una ventana controlada.

## Fase 7. Gateway redundante (ampliación)

Diseña las funciones de:

- Keepalived/VRRP para la VIP.
- nftables para forwarding y NAT.
- conntrackd para la sincronización de estado de conexiones, si el diseño lo requiere.

Registra las rutas y las reglas reales. No des por hecho que una configuración de ejemplo se ajusta a tus interfaces.

## Criterios de evaluación

- [ ] DHCPv4 entrega una dirección del pool correcto.
- [ ] Las opciones de red son coherentes.
- [ ] Las reservas se aplican como se esperaba.
- [ ] Los registros permiten seguir el proceso.
- [ ] El almacenamiento de leases está identificado.
- [ ] Los canales de control están documentados y protegidos.
- [ ] Las pruebas tienen resultados registrados.
- [ ] La configuración puede revertirse.
- [ ] No se incluyen secretos ni PDF originales en el repositorio.

## Informe final

Entrega un resumen de arquitectura, los archivos de configuración depurados, las pruebas ejecutadas, los problemas encontrados y sus soluciones. Distingue entre las pruebas realizadas y las que solo has diseñado.
