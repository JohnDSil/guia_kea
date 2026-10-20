# Errores frecuentes y diagnóstico

## 1. Error de sintaxis en la configuración

**Síntoma:** Kea no arranca o rechaza el archivo.

**Comprobaciones:**
- Revisa comas, comillas, llaves y corchetes.
- Valida JSON estricto con `jq` si el archivo es compatible.
- Comprueba que las opciones pertenecen a la versión instalada.

**Prevención:** valida los cambios antes de aplicarlos.

## 2. Interfaz incorrecta

**Síntoma:** el servicio arranca, pero no atiende a los clientes esperados.

**Comprobaciones:**

```bash
ip address
```

Confirma el nombre de la interfaz y su dirección IP.

**Prevención:** no reutilices nombres de interfaz de otro equipo sin comprobarlos.

## 3. Pool incorrecto

**Síntoma:** los clientes no reciben dirección o reciben direcciones inesperadas.

**Comprobaciones:**
- Subred y máscara.
- Límites del pool.
- Direcciones disponibles.
- Reservas y exclusiones.
- Conectividad de capa 2 entre cliente y servidor.

## 4. Reserva que no se aplica

**Síntoma:** el cliente obtiene otra dirección.

**Comprobaciones:**
- MAC y Client ID.
- Ubicación de la reserva.
- Opciones de coincidencia de identidad.
- Existencia de identidades duplicadas en máquinas clonadas.

## 5. API de control expuesta

**Síntoma:** un canal de administración es accesible desde redes que no deberían utilizarlo.

**Riesgo:** acceso a operaciones administrativas.

**Prevención:** limita las interfaces y los puertos, revisa autenticación y TLS, y evita exponer el servicio innecesariamente.

## 6. HA sin comunicación

**Síntoma:** los nodos no alcanzan un estado coherente.

**Comprobaciones:**
- Direcciones y puerto.
- Firewall.
- Nombre del servidor configurado.
- Módulo HA.
- Listener activo.
- Certificados y hora del sistema.

## 7. Gateway sin reenvío

**Síntoma:** los clientes obtienen IP, pero no alcanzan otras redes.

**Comprobaciones:**

```bash
sysctl net.ipv4.ip_forward
ip route
```

Revisa también las reglas nftables y NAT.

## 8. VIP que no conmuta

**Síntoma:** la dirección virtual no aparece en el nodo esperado.

**Comprobaciones:**
- Estado de Keepalived.
- Configuración VRRP.
- Prioridades e interfaces.
- Grupo de sincronización.
- Reglas de firewall y anuncios de la VIP.

## 9. Sesiones TCP que se interrumpen al conmutar

**Síntoma:** la nueva pasarela funciona, pero algunas conexiones existentes se pierden.

**Comprobaciones:**
- Estado de conntrackd.
- Direcciones de sincronización.
- Configuración de seguimiento de conexiones.
- Reglas y comportamiento del firewall en ambos nodos.

La sincronización de conexiones no garantiza que todas las aplicaciones mantengan sus sesiones; depende de la arquitectura y de la prueba realizada.

## 10. Método general

Ante cualquier fallo:

1. Anota el síntoma.
2. Guarda el estado actual.
3. Revisa los registros.
4. Comprueba una hipótesis cada vez.
5. Aplica un único cambio.
6. Repite la prueba.
7. Documenta la solución y la reversión.

**Regla de oro:** no confundas un servicio activo con un servicio correctamente configurado y funcional.
