# Capítulo 3. Reservas y concesiones

## Objetivos

- Distinguir las asignaciones dinámicas de las reservas.
- Comprender la identidad del cliente.
- Reconocer el ciclo de vida de una concesión.

## 1. Pool dinámico

Un pool permite que Kea asigne direcciones disponibles dentro de un rango. En el ejemplo de laboratorio, el rango dinámico es:

```text
192.168.100.100 - 192.168.100.199
```

Antes de elegirlo, reserva fuera de ese rango las direcciones que deban tener un uso fijo, como la puerta de enlace o los equipos de infraestructura.

## 2. Reservas

Una reserva vincula una identidad de cliente con parámetros de asignación, como una dirección IPv4 específica.

Ejemplo orientativo de una reserva por dirección MAC:

```json
{
  "reservations": [
    {
      "hw-address": "02:00:00:00:00:11",
      "ip-address": "192.168.100.11"
    },
    {
      "hw-address": "02:00:00:00:00:12",
      "ip-address": "192.168.100.12"
    }
  ]
}
```

Este bloque debe colocarse en el contexto que corresponda a la configuración real. Verifica en el manual de tu versión dónde se declaran las reservas y cómo se evalúan.

En el material de estudio aparecen las opciones `reservations-global: false` y `reservations-out-of-pool: true`. La segunda permite reservas fuera de los pools dinámicos cuando se cumplen las condiciones de configuración correspondientes.

## 3. Identidad del cliente

La opción:

```json
"match-client-id": false
```

aparece en el laboratorio del material de estudio para evitar que la identificación mediante Client ID genere confusión en máquinas virtuales clonadas. El comportamiento exacto depende de cómo se identifique al cliente y de la versión de Kea.

No asumas que dos clientes con la misma identidad son equipos independientes. Comprueba sus MAC, Client ID y comportamiento de clonación.

## 4. Ciclo de vida de una concesión

Una concesión (*lease*) representa una dirección asignada a un cliente durante un periodo. Puede renovarse, expirar o liberarse.

El material también presenta el ajuste:

```json
"expired-leases-processing": {
  "hold-reclaimed-time": 1296000
}
```

`1296000` segundos equivalen a 15 días. Este parámetro está relacionado con el tiempo que se conservan las concesiones recuperadas antes de su eliminación definitiva. Comprueba el efecto y los requisitos de la versión utilizada.

## 5. Liberación de direcciones

El material estudia una clase de clientes que descarta mensajes DHCPv4 de tipo `7`, asociados a DHCPRELEASE:

```json
{
  "client-classes": [
    {
      "name": "DROP",
      "test": "pkt4.msgtype == 7"
    }
  ]
}
```

**No añadas esta regla sin entender su efecto.** Descartar mensajes de liberación modifica el comportamiento normal del servicio y puede hacer que una dirección permanezca asignada durante más tiempo. Debe probarse en un entorno aislado y justificarse según el objetivo del laboratorio.

## Ejercicios

1. ¿Qué diferencia hay entre una reserva y una dirección del pool dinámico?
2. ¿Por qué una reserva fuera del pool puede resultar útil?
3. ¿Cuántos días representan 1296000 segundos?
4. ¿Qué riesgo operativo tiene descartar mensajes DHCPRELEASE?
5. ¿Qué datos comprobarías si dos máquinas virtuales parecen tener la misma identidad?

## Checklist

- [ ] El pool no se solapa de forma accidental con las direcciones de infraestructura.
- [ ] Las reservas utilizan identificadores correctos.
- [ ] Comprendo el uso de `match-client-id`.
- [ ] He revisado la duración de las concesiones y su recuperación.
- [ ] No he aplicado reglas de descarte sin probar sus efectos.
