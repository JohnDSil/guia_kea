# Capítulo 6. Seguridad de Kea

## Objetivos

- Identificar las amenazas sobre los canales de control.
- Comprender la finalidad de TLS y la autenticación mutua.
- Preparar una revisión de seguridad.

## 1. Riesgo de HTTP sin protección

El material advierte que una API de control accesible por HTTP sin autenticación ni cifrado puede permitir que quien alcance el puerto envíe comandos administrativos.

Las consecuencias dependen de los comandos disponibles y de los permisos efectivos, pero el principio de seguridad es claro: una interfaz de control no debe tratarse como un servicio público.

## 2. Separar los canales

La estrategia de seguridad depende de la función de cada canal:

- **Administración local:** limitar los permisos del socket Unix.
- **Comunicación HA:** proteger el listener dedicado y utilizar TLS mutuo cuando corresponda.
- **Administración remota:** limitar el acceso de red y proteger la interfaz de control con los mecanismos admitidos por la versión.

El material identifica como riesgo la posibilidad de que un atacante alcance o intercepte la comunicación entre pares HA y manipule mensajes o estados si no existe protección adecuada.

## 3. Lista de comprobación

Antes de habilitar la administración remota:

- [ ] Identifica qué interfaces y direcciones escuchan.
- [ ] Limita los puertos de control a los equipos autorizados.
- [ ] Verifica el cifrado y la autenticación admitidos por tu versión.
- [ ] Comprueba certificados, confianza y autenticación mutua si se usan.
- [ ] Revisa los permisos de los sockets locales.
- [ ] Evita exponer los canales de administración a redes de usuarios.
- [ ] Registra los cambios y prepara una forma de recuperar el acceso.

## 4. Documentación según versión

Comprueba la versión:

```bash
kea-dhcp4 -V
```

Consulta en el manual correspondiente los apartados sobre:

- Securing Communication Between HA Partners.
- Securing the Control Agent.

Los nombres exactos de las secciones pueden variar según la edición del manual.

## Ejercicios

1. Explica la diferencia entre cifrado y autenticación.
2. ¿Por qué el TLS mutuo es relevante para la comunicación HA?
3. ¿Qué riesgo existe si el puerto de control es accesible desde toda la red?
4. Diseña una política de acceso para administración local y remota.

## Checklist

- [ ] He inventariado todos los canales de control.
- [ ] He restringido el acceso de red.
- [ ] He revisado la autenticación y el cifrado.
- [ ] He consultado el manual de la versión instalada.
- [ ] He comprobado que la administración sigue funcionando tras endurecer la seguridad.
