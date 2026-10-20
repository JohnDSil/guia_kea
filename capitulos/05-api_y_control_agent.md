# Capítulo 5. API y Control Agent

## Objetivos

- Distinguir los canales de control de Kea.
- Comprender la función del Control Agent.
- Reconocer los riesgos de la administración remota.

## 1. Tres vías de control

El material distingue tres vías:

| Vía | Uso principal | Consideración |
|---|---|---|
| Socket de control Unix | Administración local | Protege el acceso mediante permisos del sistema de archivos |
| Listener dedicado para HA | Comunicación entre pares HA | Debe protegerse de acuerdo con el diseño y la versión |
| `kea-ctrl-agent` | Control HTTP/JSON remoto | Requiere protección de red y medidas de seguridad |

No son vías intercambiables sin más: tienen propósitos y mecanismos de protección distintos.

## 2. Control Agent

El Control Agent ofrece una interfaz HTTP/JSON para enviar comandos de administración a los servicios Kea configurados para ello.

Un riesgo importante es exponer una interfaz de control accesible por la red sin cifrado ni autenticación suficientes. Si un tercero obtiene acceso a ella, podría ejecutar operaciones administrativas no autorizadas.

## 3. Socket local

Para la administración local, el material describe el uso de un socket Unix y herramientas como `socat`. La ruta del socket y el formato de la petición dependen de la configuración.

No inventes una ruta de socket: localízala en el archivo de configuración del servicio y consulta la documentación de tu versión.

## 4. Comprobación de versión

Consulta la versión instalada:

```bash
kea-dhcp4 -V
```

Después, revisa el manual correspondiente. Las opciones y la arquitectura de control pueden cambiar entre versiones mayores. En particular, el material advierte que para Kea 3.x debe comprobarse la situación del socket HTTP integrado y la posible obsolescencia del Control Agent.

No retires un componente basándote únicamente en esa nota: confirma qué funciones y migraciones se aplican a tu instalación.

## Ejercicios

1. ¿Qué diferencia hay entre un socket Unix y una API HTTP?
2. ¿Por qué el Control Agent no debería quedar expuesto sin protección?
3. ¿Qué comprobarías antes de copiar un ejemplo de API?
4. ¿Por qué es importante identificar la versión de Kea?

## Checklist

- [ ] Sé qué canal de control usa mi laboratorio.
- [ ] He localizado su configuración real.
- [ ] No expongo la API innecesariamente.
- [ ] He comprobado la versión y el manual correspondiente.
