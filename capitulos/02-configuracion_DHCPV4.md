# Capítulo 2. Configuración de DHCPv4

## Objetivos

- Identificar las secciones de una configuración DHCPv4.
- Definir interfaz, subred, pool y opciones.
- Validar el archivo antes de aplicar cambios.

## 1. Estructura de configuración

Los archivos de Kea usan una estructura basada en JSON. En una configuración DHCPv4 son habituales bloques para las interfaces, los parámetros generales, las subredes, las opciones DHCP, el almacenamiento y el registro.

Ejemplo didáctico basado en el material de estudio:

```json
{
  "Dhcp4": {
    "interfaces-config": {
      "interfaces": [ "enp0s8" ],
      "dhcp-socket-type": "raw"
    },
    "valid-lifetime": 4000,
    "renew-timer": 1000,
    "rebind-timer": 2000,
    "subnet4": [
      {
        "subnet": "192.168.100.0/24",
        "pools": [
          {
            "pool": "192.168.100.100 - 192.168.100.199"
          }
        ],
        "option-data": [
          {
            "name": "routers",
            "data": "192.168.100.1"
          },
          {
            "name": "domain-name-servers",
            "data": "9.9.9.9"
          },
          {
            "name": "domain-name",
            "data": "dominio-100.test"
          }
        ]
      }
    ]
  }
}
```

Este ejemplo es una plantilla de estudio, no una configuración universal. La interfaz debe existir y la dirección del router debe corresponder a la red real del laboratorio.

## 2. Conceptos importantes

- **Subred:** define el segmento de red atendido por Kea.
- **Pool:** rango de direcciones que el servidor puede asignar dinámicamente.
- **`valid-lifetime`:** duración de la concesión, en segundos.
- **`renew-timer`:** tiempo a partir del cual el cliente intenta renovar.
- **`rebind-timer`:** momento en el que el cliente puede intentar renovar con otro servidor.
- **`option-data`:** opciones entregadas al cliente, como router, DNS o dominio.

En el ejemplo, la concesión dura 4000 segundos. Los valores de temporizadores deben ser coherentes entre sí y con los requisitos del entorno.

## 3. Validar el archivo

Si el archivo utiliza JSON estricto:

```bash
jq . kea-dhcp4.conf
```

En Vim, el contenido puede formatearse con:

```vim
:%!jq .
```

Kea admite determinadas extensiones al formato JSON, por lo que un archivo que utiliza esas extensiones puede no pasar por `jq`. La validación con `jq` tampoco sustituye a la comprobación que realiza Kea sobre sus propias opciones.

## 4. Procedimiento seguro

1. Haz una copia del archivo actual.
2. Edita una sola parte de la configuración.
3. Comprueba la sintaxis.
4. Valida el archivo con el mecanismo admitido por tu versión de Kea.
5. Aplica el cambio siguiendo el procedimiento de tu distribución.
6. Comprueba el estado del servicio y los registros.

## Ejercicios

1. Cambia el pool a `192.168.100.120 - 192.168.100.180`.
2. Explica qué ocurre si se configura una interfaz que no existe.
3. Calcula cuántos segundos son 4000 segundos en minutos.
4. Explica la diferencia entre el pool y la subred.

## Checklist

- [ ] La interfaz es correcta.
- [ ] La subred coincide con el laboratorio.
- [ ] El pool pertenece a la subred.
- [ ] Las opciones de router y DNS son coherentes.
- [ ] He validado el archivo antes de aplicarlo.
