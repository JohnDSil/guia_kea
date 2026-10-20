# Capítulo 7. Alta disponibilidad de Kea

## Objetivos

- Comprender el propósito de la alta disponibilidad.
- Identificar los parámetros que deben coincidir con la topología.
- Reconocer fallos de comunicación entre pares.

## 1. Concepto

La alta disponibilidad (HA) busca mantener el servicio cuando uno de los nodos deja de estar disponible. En Kea, los nodos deben comunicarse mediante el mecanismo HA configurado y mantener estados compatibles con la topología.

La redundancia no se demuestra únicamente porque ambos servicios estén activos: hay que verificar la comunicación, el estado informado y el comportamiento durante un fallo.

## 2. Elementos que revisar

El material de estudio destaca los siguientes puntos:

- Nombre de cada servidor configurado en `this-server-name`.
- Dirección y puerto del peer.
- Conectividad entre los nodos.
- Disponibilidad del módulo `libdhcp_ha.so`.
- Estado del listener de control correspondiente.
- Configuración TLS y certificados cuando se utilizan.
- Sincronización horaria.
- Estado de HA devuelto por los comandos de control.

Un nombre de servidor que no coincide con la configuración del peer puede impedir que el entorno funcione como se espera.

## 3. Diagnóstico inicial

Comprueba primero los aspectos básicos:

1. ¿Resuelven o alcanzan los nodos sus direcciones configuradas?
2. ¿Está escuchando el puerto esperado?
3. ¿Permite el firewall la comunicación entre los peers?
4. ¿Está disponible el módulo HA?
5. ¿Coinciden los nombres y las direcciones configuradas?
6. ¿Es correcta la configuración TLS?
7. ¿Se encuentran los relojes sincronizados?

En el laboratorio de referencia se menciona el puerto `8000`, pero no debe asumirse que es el puerto correcto para cualquier despliegue.

## 4. Pruebas controladas

Realiza las pruebas en una red aislada:

- Comprueba el estado inicial de ambos nodos.
- Verifica que la comunicación HA funciona.
- Interrumpe un nodo siguiendo un plan de prueba.
- Observa el comportamiento del servicio y del cliente.
- Recupera el nodo y verifica la convergencia de estados.

No provoques una conmutación en producción sin un plan de mantenimiento y recuperación.

## Ejercicios

1. ¿Por qué dos servicios activos no garantizan por sí solos una HA funcional?
2. ¿Qué investigarías si el peer no responde?
3. ¿Qué función tiene `this-server-name`?
4. Diseña una prueba para comprobar el comportamiento durante la caída de un nodo.

## Checklist

- [ ] Los nombres de los nodos coinciden con la configuración.
- [ ] La conectividad entre peers funciona.
- [ ] El listener y el módulo HA están disponibles.
- [ ] La protección TLS se ha verificado cuando corresponde.
- [ ] Los estados iniciales son coherentes.
- [ ] La conmutación se prueba en laboratorio.
