# Ruta de aprendizaje de Kea DHCP

## Fase 1. Comprender el servicio

**Capítulo 1 — Introducción a Kea**

Objetivos:
- Entender qué función cumple un servidor DHCP.
- Reconocer los componentes principales de Kea.
- Identificar los servicios y sus archivos de configuración.
- Comprender el papel de Stork y de la API de control.

Criterio para avanzar: explicar qué servicio se encarga de DHCPv4, dónde se configura y cómo se administra.

## Fase 2. Configurar DHCPv4

**Capítulo 2 — Configuración de DHCPv4**

Objetivos:
- Reconocer las secciones principales del archivo de configuración.
- Definir una subred, un pool y opciones de red.
- Validar la sintaxis y comprobar el servicio.

Criterio para avanzar: poder explicar cada bloque de una configuración de laboratorio.

## Fase 3. Controlar las asignaciones

**Capítulo 3 — Reservas y leases**

Objetivos:
- Diferenciar un pool dinámico de una reserva.
- Comprender el tiempo de concesión.
- Entender el efecto de `match-client-id`.
- Reconocer el procesamiento de concesiones expiradas.

Criterio para avanzar: diseñar una subred de prueba con un pool y reservas coherentes.

## Fase 4. Diagnosticar el servicio

**Capítulo 4 — Registros y almacenamiento**

Objetivos:
- Identificar niveles de log.
- Localizar el almacenamiento de leases.
- Reconocer eventos de inicio, asignación y liberación.
- Comprender las diferencias entre almacenamiento en memoria y persistente.

Criterio para avanzar: explicar cómo investigar una asignación que no aparece en el registro esperado.

## Fase 5. Administrar Kea

**Capítulo 5 — API y Control Agent**

Objetivos:
- Diferenciar el socket de control local, el canal HA y la API HTTP/JSON.
- Comprender el papel de `kea-ctrl-agent`.
- Reconocer los riesgos de exponer una interfaz de control.

Criterio para avanzar: dibujar qué componente usarías para una administración local y cuál para una administración remota.

## Fase 6. Proteger el plano de control

**Capítulo 6 — Seguridad**

Objetivos:
- Identificar los riesgos de HTTP sin cifrado ni autenticación.
- Entender el propósito de TLS y la autenticación mutua.
- Limitar el acceso a las interfaces de administración.
- Verificar las recomendaciones aplicables a la versión instalada.

Criterio para avanzar: elaborar una lista de comprobación de seguridad antes de exponer un puerto de control.

## Fase 7. Preparar alta disponibilidad

**Capítulo 7 — Alta disponibilidad de Kea**

Objetivos:
- Comprender el papel de los nodos primario y secundario.
- Identificar los parámetros que deben coincidir con la topología.
- Reconocer los problemas de conectividad y estado entre pares.

Criterio para avanzar: verificar que ambos nodos se reconocen y reportan un estado coherente.

## Fase 8. Integrar la redundancia de red

**Capítulo 8 — Gateway y redundancia**

Objetivos:
- Comprender el papel de una VIP con Keepalived/VRRP.
- Distinguir la redundancia del gateway de la HA de Kea.
- Entender el propósito de conntrackd y de las reglas de NAT/forwarding.

Criterio para avanzar: poder explicar qué componente mantiene cada tipo de estado.

## Fase 9. Probar

**Capítulo 9 — Verificación y pruebas**

Objetivos:
- Validar configuraciones.
- Comprobar servicios y conectividad.
- Probar renovaciones DHCP.
- Diseñar una prueba controlada de conmutación.

Criterio para avanzar: ejecutar un plan de pruebas y anotar resultados observables.

## Fase 10. Diagnosticar fallos

**Capítulo 10 — Resolución de problemas**

Objetivos:
- Separar errores de configuración, servicio, red y HA.
- Seguir una secuencia de diagnóstico reproducible.
- Evitar cambios simultáneos que dificulten identificar la causa.

Criterio final: resolver un escenario de laboratorio documentando síntomas, hipótesis, pruebas y solución.

## Método de estudio recomendado

Para cada capítulo:

1. Lee los objetivos.
2. Resume los conceptos con tus propias palabras.
3. Reproduce los ejemplos en un laboratorio.
4. Cambia un parámetro y observa su efecto.
5. Realiza los ejercicios sin mirar las soluciones.
6. Registra los comandos y resultados que hayas comprobado realmente.

No ejecutes pruebas de fallo, cambios de firewall ni conmutaciones en producción sin una ventana de mantenimiento y un plan de recuperación.
