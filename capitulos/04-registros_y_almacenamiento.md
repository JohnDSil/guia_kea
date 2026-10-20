# Capítulo 4. Registros y almacenamiento

## Objetivos

- Reconocer los niveles de registro.
- Identificar los eventos DHCP importantes.
- Comprender las opciones de almacenamiento de leases.

## 1. Niveles de log

Los niveles de registro que aparecen en el material son:

| Nivel | Uso general |
|---|---|
| `DEBUG` | Información detallada para investigar problemas |
| `INFO` | Eventos informativos |
| `WARN` | Situaciones que requieren atención |
| `ERROR` | Errores que afectan a una operación |
| `FATAL` | Fallos críticos |

Usa el nivel de detalle adecuado para la investigación. Los registros muy detallados pueden generar mucho volumen.

## 2. Eventos de DHCPv4

Entre los nombres de eventos que se estudian están:

- `DHCP4_STARTED`: inicio del servicio DHCPv4.
- `DHCP4_LEASE_ADVERT`: evento relacionado con el anuncio de una concesión.
- `DHCP4_LEASE_ALLOC`: asignación de una concesión.
- `DHCP4_RELEASE`: liberación de una concesión.

Los mensajes exactos y su formato pueden cambiar entre versiones.

## 3. Almacenamiento de concesiones

El material presenta tres tipos de backend:

- `memfile`
- MySQL
- PostgreSQL

`memfile` es el backend basado en archivos mencionado como predeterminado en el material. La ruta de leases IPv4 que se muestra es:

```text
/var/lib/kea/kea-leases4.csv
```

No des por hecho que todos los sistemas usan esa ruta: comprueba la configuración instalada.

El parámetro `lfc-interval` controla el intervalo asociado al proceso de limpieza del archivo de leases. El valor predeterminado descrito en el material es de una hora.

## 4. Diagnóstico básico

Al investigar una asignación que no funciona:

1. Comprueba que el servicio ha arrancado.
2. Revisa los errores de configuración.
3. Confirma que el servidor escucha en la interfaz prevista.
4. Comprueba si llegan solicitudes de los clientes.
5. Busca los eventos relacionados con la concesión.
6. Revisa el backend de almacenamiento configurado.

Ejemplo de consulta de estado en sistemas con systemd:

```bash
systemctl status kea-dhcp4-server
```

El nombre del servicio puede variar según el sistema operativo o el paquete instalado.

## Ejercicios

1. ¿Qué nivel de log usarías para una investigación detallada?
2. ¿Qué diferencia hay entre un error y una advertencia?
3. ¿Dónde buscarías las concesiones si el sistema utiliza el archivo mencionado?
4. ¿Por qué no debes asumir que la ruta del archivo es idéntica en todas las distribuciones?

## Checklist

- [ ] Sé distinguir los niveles de log.
- [ ] Reconozco los eventos DHCP estudiados.
- [ ] Sé qué backend está configurado.
- [ ] He verificado la ruta real de almacenamiento.
- [ ] Relaciono los registros con el estado del servicio.
