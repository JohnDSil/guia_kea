# Capítulo 1. Introducción a Kea

## Objetivos

- Comprender la función de Kea DHCP.
- Identificar sus servicios principales.
- Localizar los archivos de configuración.
- Entender la administración mediante API.

## 1. ¿Qué es Kea?

Kea es un servidor DHCP desarrollado por Internet Systems Consortium (ISC). Permite asignar parámetros de red a clientes mediante DHCP para IPv4 e IPv6.

Los materiales de estudio presentan Kea como alternativa moderna a ISC DHCP, cuyo mantenimiento terminó en 2022.

## 2. Componentes principales

| Servicio | Función | Archivo habitual |
|---|---|---|
| `kea-dhcp4-server` | DHCP para IPv4 | `/etc/kea/kea-dhcp4.conf` |
| `kea-dhcp6-server` | DHCP para IPv6 | `/etc/kea/kea-dhcp6.conf` |
| `kea-dhcp-ddns-server` | Actualizaciones DNS dinámicas | `/etc/kea/kea-dhcp-ddns.conf` |
| `kea-ctrl-agent` | Interfaz HTTP/JSON de control | `/etc/kea/kea-ctrl-agent.conf` |

La disponibilidad y organización de los paquetes dependen de la distribución y la versión.

## 3. Arquitectura modular

Kea separa funciones en componentes. Esto permite desplegar los servicios necesarios sin tener que ejecutar todas las funciones en un único proceso.

La administración puede realizarse por distintos canales de control. No todos ofrecen las mismas propiedades de seguridad ni están destinados al mismo uso.

Stork es una aplicación web de supervisión y gestión del entorno Kea y puede trabajar también con BIND9.

## 4. Documentación y versiones

Documentación oficial:

https://kea.readthedocs.io/en/latest/

Antes de copiar una configuración, comprueba la versión instalada y consulta su manual. Una opción válida en una versión puede no existir o comportarse de forma distinta en otra.

## Ejercicios

1. Explica la función de `kea-dhcp4-server`.
2. ¿Qué diferencia hay entre el servidor DHCP y el Control Agent?
3. ¿Para qué puede utilizarse Stork?
4. ¿Por qué no conviene copiar opciones de una guía sin comprobar la versión?

## Checklist

- [ ] Identifico los servicios principales.
- [ ] Sé localizar sus archivos de configuración.
- [ ] Sé dónde consultar la documentación oficial.
- [ ] Distingo el servicio DHCP de su interfaz de administración.
