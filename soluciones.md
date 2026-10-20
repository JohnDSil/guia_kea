# Soluciones orientativas

Estas respuestas sirven como referencia. En los ejercicios prácticos, la solución válida depende de la configuración y de los resultados reales del laboratorio.

## Bloque A. Conceptos

1. `kea-dhcp4-server` atiende DHCPv4; `kea-dhcp6-server`, DHCPv6; `kea-dhcp-ddns-server` gestiona la función DHCP-DDNS; `kea-ctrl-agent` proporciona una interfaz HTTP/JSON de control en las versiones y arquitecturas que lo utilizan.
2. La subred define el segmento atendido. El pool delimita las direcciones disponibles para asignaciones dinámicas.
3. Una reserva asocia un cliente identificado con una asignación prevista; una concesión dinámica se obtiene del pool.
4. `DEBUG` ofrece información más detallada para investigar; `ERROR` registra errores que afectan a una operación.
5. La API puede permitir operaciones administrativas y, por ello, no debe ser accesible sin controles apropiados.

## Bloque B. Configuración

6. El pool quedaría así:

   ```json
   {
     "pool": "192.168.100.120 - 192.168.100.180"
   }
   ```

7. El valor del dominio sería `laboratorio.test`.
8. El router debe existir y ser alcanzable desde la subred de los clientes.
9. Ejecuta `jq . kea-dhcp4.conf`. Si el archivo utiliza extensiones propias de Kea, comprueba también la configuración con los mecanismos adecuados para esa versión.
10. Verifica sintaxis, opciones admitidas, interfaces, direccionamiento, disponibilidad del pool y registros tras aplicar el cambio.

## Bloque C. Reservas y concesiones

11. Reserva orientativa:

   ```json
   {
     "hw-address": "02:00:00:00:00:21",
     "ip-address": "192.168.100.21"
   }
   ```

   Debe integrarse en el bloque de reservas correcto de la configuración.

12. Comprueba MAC, Client ID y el parámetro `match-client-id`. Confirma si las máquinas clonadas comparten identificadores.
13. `1296000 / 86400 = 15 días`.
14. Descartar DHCPRELEASE puede impedir que el servidor procese la liberación normal y prolongar la ocupación de una dirección.

## Bloque D. Seguridad

15. El socket Unix sirve para control local mediante permisos; el listener HA comunica los peers; el Control Agent ofrece una interfaz HTTP/JSON en los despliegues que lo utilizan.
16. Restringe el acceso por red, limita las direcciones autorizadas, utiliza los mecanismos de cifrado y autenticación admitidos y verifica los registros.
17. Comprueba la versión exacta y el manual correspondiente antes de usar una opción o procedimiento.
18. TLS mutuo permite que ambas partes autentiquen a su peer y protege la comunicación frente a observación o manipulación durante el transporte, siempre que esté correctamente configurado y validado.

## Bloque E. Alta disponibilidad

19. Kea proporciona el servicio DHCP; el gateway reenvía tráfico entre redes. Son componentes distintos y deben probarse por separado.
20. Muestra el valor de `net.ipv4.ip_forward`, que indica si está habilitado el reenvío IPv4.
21. Necesitas origen, interfaz de entrada, interfaz de salida, destino de traducción, rutas y reglas de firewall.
22. conntrackd sincroniza estado de seguimiento de conexiones en el diseño descrito.
23. Registra el estado normal de ambos nodos, provoca un fallo controlado, observa DHCP y la conectividad, recupera el nodo y confirma el estado final.

## Práctica integradora

La solución se considera correcta cuando las pruebas tienen evidencias reproducibles y se documentan las diferencias respecto a lo esperado. No es suficiente presentar archivos de configuración sin demostrar su funcionamiento.
