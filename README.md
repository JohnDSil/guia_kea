# Guía de Kea DHCP

Guía de estudio y práctica sobre **ISC Kea DHCP**, su configuración, las reservas, el almacenamiento de concesiones (*leases*), la API de control, la seguridad, la alta disponibilidad y la resolución de problemas.

El contenido se ha organizado a partir de los materiales de estudio proporcionados. Los PDF originales no forman parte de este repositorio.

## Contenido

### Introducción y configuración

1. [Introducción a Kea](capitulos/01-introduccion_a_kea.md)
2. [Configuración de DHCPv4](capitulos/02-configuracion_DHCPV4.md)
3. [Reservas y concesiones](capitulos/03-reservas_y_leases.md)
4. [Registros y almacenamiento](capitulos/04-registros_y_almacenamiento.md)

### Administración y seguridad

5. [API y Control Agent](capitulos/05-api_y_control_agent.md)
6. [Seguridad de Kea](capitulos/06-seguridad_de_kea.md)

### Alta disponibilidad y resolución de problemas

7. [Alta disponibilidad de Kea](capitulos/07-alta_disponibilidad.md)
8. [Gateway y redundancia de red](capitulos/08-gateway_y_redundancia.md)
9. [Verificación y pruebas](capitulos/09-verificacion_y_pruebas.md)
10. [Resolución de problemas](capitulos/10-resolucion_de_problemas.md)

### Material complementario

- [Ruta de aprendizaje](ruta_de_aprendizaje.md)
- [Ejercicios](ejercicios.md)
- [Práctica integradora](practica_integradora.md)
- [Soluciones orientativas](soluciones.md)
- [Errores frecuentes](errores_frecuentes.md)

## Cómo utilizar la guía

1. Sigue los capítulos en orden.
2. Escribe y valida las configuraciones en un laboratorio aislado.
3. Realiza los ejercicios sin consultar primero las soluciones.
4. Completa la práctica integradora.
5. Comprueba los servicios y los registros después de cada cambio.

## Requisitos del laboratorio

- Una máquina Linux para instalar y configurar Kea.
- Acceso administrativo mediante `sudo`.
- Una interfaz de red de laboratorio.
- Un cliente DHCP de prueba.
- Para los capítulos de alta disponibilidad: dos nodos Kea y una topología de red que permita probar la redundancia.

Los nombres de interfaces, direcciones IP, paquetes y opciones pueden variar según la distribución y la versión instalada.

## Validación de configuraciones

Kea utiliza archivos de configuración con sintaxis basada en JSON y admite algunas extensiones. Para comprobar la sintaxis JSON estricta de un archivo compatible:

```bash
jq . kea-dhcp4.conf
```

La validación sintáctica no garantiza que todas las opciones sean válidas para la versión instalada de Kea. Consulta también su documentación correspondiente.

## Documentación oficial

- https://kea.readthedocs.io/en/latest/

## Alcance

Esta guía es material de estudio. Antes de aplicar una configuración en producción, verifica las opciones con el manual de referencia de la versión instalada, especialmente en los apartados de API, seguridad y alta disponibilidad.
