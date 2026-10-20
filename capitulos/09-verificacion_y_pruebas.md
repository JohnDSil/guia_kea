# Capítulo 9. Verificación y pruebas

## Objetivos

- Validar los cambios antes de aplicarlos.
- Comprobar el estado de Kea y la conectividad.
- Verificar asignaciones DHCP y alta disponibilidad.

## 1. Validación por capas

Es preferible verificar una capa cada vez.

### Capa 1: configuración

```bash
jq . /etc/kea/kea-dhcp4.conf
```

Esto comprueba sintaxis JSON estricta. Si la configuración utiliza extensiones admitidas por Kea, el resultado puede no ser válido como JSON estricto.

### Capa 2: servicio

```bash
systemctl status kea-dhcp4-server
```

Adapta el nombre del servicio a tu distribución. Comprueba también los registros del arranque y los errores de configuración.

### Capa 3: red

```bash
ip address
ip route
```

Confirma que la interfaz prevista está activa y que el direccionamiento coincide con el laboratorio.

### Capa 4: cliente DHCP

En un cliente de laboratorio, verifica que recibe una dirección del pool correcto, junto con las opciones de router y DNS previstas.

No realices renovaciones forzadas ni liberes concesiones en un equipo que dependa de esa dirección para mantener una conexión crítica.

### Capa 5: alta disponibilidad

Verifica el estado de ambos nodos mediante el mecanismo de control configurado. El comando exacto depende de la versión y del canal de control disponible.

## 2. Plan de pruebas

| Prueba | Resultado esperado |
|---|---|
| Arranque de Kea | Servicio activo sin errores críticos |
| Cliente nuevo | Recibe una dirección válida |
| Opciones DHCP | Router y DNS coinciden con el diseño |
| Reserva | Cliente identificado recibe la dirección prevista |
| Reinicio controlado | Servicio vuelve a funcionar |
| Fallo de un nodo HA | Comportamiento acorde con el modo HA configurado |
| Conmutación del gateway | La VIP y el encaminamiento siguen el diseño |
| Recuperación | Los nodos vuelven a un estado coherente |

Los resultados deben anotarse; no marques una prueba como superada solo porque el servicio figure como activo.

## 3. Registro de resultados

Para cada prueba, apunta:

- Fecha y versión de Kea.
- Configuración probada.
- Acción realizada.
- Resultado esperado.
- Resultado observado.
- Mensajes relevantes.
- Conclusión y cambios aplicados.

## Ejercicios

1. Explica por qué `jq` no valida todas las opciones semánticas de Kea.
2. ¿Qué comprobarías si el servicio está activo, pero el cliente no obtiene una IP?
3. ¿Qué evidencias registrarías durante una prueba de conmutación?
4. Diseña una tabla de pruebas para tu propio laboratorio.

## Checklist

- [ ] He validado la configuración.
- [ ] He comprobado el servicio.
- [ ] He verificado las interfaces y las rutas.
- [ ] He probado un cliente DHCP.
- [ ] He revisado los registros.
- [ ] He documentado los resultados.
