# DNS y DHCP

## Introducción

En una red local no basta con conectar dispositivos físicamente. También es necesario que cada dispositivo tenga una dirección IP válida y que pueda encontrar servicios por nombre.

Para eso se usan dos servicios fundamentales:

```txt
DHCP -> Asigna direcciones IP automáticamente.
DNS  -> Traduce nombres de dominio a direcciones IP.
```

Ambos servicios son esenciales en redes domésticas, escolares, empresariales y de laboratorio.

## ¿Qué es DHCP?

DHCP significa:

```txt
Dynamic Host Configuration Protocol
```

En español:

```txt
Protocolo de configuración dinámica de host
```

DHCP permite que un dispositivo reciba automáticamente la configuración necesaria para conectarse a una red.

Sin DHCP, el administrador tendría que configurar manualmente en cada dispositivo:

- Dirección IP.
- Máscara de subred.
- Puerta de enlace.
- Servidores DNS.

## Ejemplo sin DHCP

Si una red no tiene DHCP, cada equipo debe configurarse manualmente.

Ejemplo para una laptop:

```txt
IP:              192.168.10.25
Máscara:         255.255.255.0
Gateway:         192.168.10.1
DNS primario:    192.168.10.1
DNS secundario:  8.8.8.8
```

Esto funciona, pero no es práctico cuando hay muchos dispositivos.

También aumenta el riesgo de errores, por ejemplo:

- Dos dispositivos con la misma IP.
- Gateway incorrecto.
- Máscara incorrecta.
- DNS mal configurado.

## Ejemplo con DHCP

Con DHCP, el dispositivo solicita configuración automáticamente.

Proceso simplificado:

```txt
1. El dispositivo se conecta a la red.
2. Solicita una dirección IP.
3. El servidor DHCP responde con una IP disponible.
4. El dispositivo recibe máscara, gateway y DNS.
5. El dispositivo puede comunicarse en la red.
```

Ejemplo de configuración asignada automáticamente:

```txt
IP asignada:     192.168.10.105
Máscara:         255.255.255.0
Gateway:         192.168.10.1
DNS:             192.168.10.1
```

## ¿Quién entrega DHCP?

En redes domésticas, normalmente el router del proveedor entrega DHCP.

En redes más avanzadas, DHCP puede ser entregado por:

- Router.
- Firewall.
- Servidor dedicado.
- Controlador de red.
- Servidor Linux o Windows Server.
- pfSense, OPNsense, MikroTik, UniFi, Omada, entre otros.

## Rango DHCP

Un rango DHCP define qué direcciones IP puede entregar automáticamente el servidor DHCP.

Ejemplo:

```txt
Red:         192.168.10.0/24
Gateway:     192.168.10.1
Rango DHCP:  192.168.10.100 - 192.168.10.199
```

Esto significa que los dispositivos recibirán IPs dentro de ese rango.

Ejemplo:

```txt
Laptop:      192.168.10.100
Celular:     192.168.10.101
Tablet:      192.168.10.102
```

## Direcciones reservadas

No todas las direcciones deben entregarse por DHCP.

Algunas direcciones se reservan para equipos importantes.

Ejemplo:

| Dirección | Uso |
|---|---|
| 192.168.10.1 | Gateway / router |
| 192.168.10.10 | Switch administrable |
| 192.168.10.20 | Impresora |
| 192.168.10.30 | Servidor local |
| 192.168.10.100-199 | Rango DHCP |

Esto ayuda a evitar conflictos.

## DHCP por segmento

Si la red está segmentada, cada segmento debe tener su propio rango DHCP.

Ejemplo:

| Segmento | Red | Gateway | Rango DHCP |
|---|---|---|---|
| Red principal | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.100-199 |
| Red invitados | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.100-199 |
| Red IoT | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.100-199 |
| Red servidores | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.100-199 |

Cada red tiene su propio gateway y su propio rango de direcciones.

## ¿Qué es DNS?

DNS significa:

```txt
Domain Name System
```

En español:

```txt
Sistema de nombres de dominio
```

DNS sirve para traducir nombres fáciles de recordar a direcciones IP.

Por ejemplo, los humanos usamos:

```txt
google.com
github.com
servidor-local.lan
```

Pero las computadoras necesitan direcciones IP.

DNS permite convertir un nombre en una IP.

Ejemplo:

```txt
github.com -> 140.82.112.3
```

## ¿Por qué se necesita DNS?

Sin DNS, tendríamos que recordar direcciones IP.

Sería poco práctico escribir:

```txt
140.82.112.3
```

en lugar de:

```txt
github.com
```

DNS hace que la navegación y el acceso a servicios sean más simples.

## DNS en una red local

En una red local, DNS también puede servir para encontrar servicios internos.

Ejemplo:

```txt
servidor-web.local -> 192.168.40.10
impresora.local    -> 192.168.10.20
nas.local          -> 192.168.40.20
```

Esto permite que los usuarios accedan a servicios por nombre en lugar de memorizar IPs.

## Relación entre DNS y DHCP

DHCP y DNS trabajan juntos.

DHCP puede entregar a los dispositivos la dirección del servidor DNS que deben usar.

Ejemplo:

```txt
IP asignada:  192.168.10.105
Gateway:      192.168.10.1
DNS:          192.168.10.1
```

En este caso, el dispositivo usará `192.168.10.1` como servidor DNS.

## Ejemplo completo de configuración DHCP

Para la red principal:

```txt
Red:              192.168.10.0/24
Gateway:          192.168.10.1
Rango DHCP:       192.168.10.100 - 192.168.10.199
DNS interno:      192.168.10.1
DNS secundario:   8.8.8.8
```

Un dispositivo podría recibir:

```txt
IP:          192.168.10.101
Máscara:     255.255.255.0
Gateway:     192.168.10.1
DNS:         192.168.10.1
```

## DHCP estático o reserva DHCP

Una reserva DHCP permite que un dispositivo reciba siempre la misma IP automáticamente.

Esto se hace asociando una dirección MAC con una IP.

Ejemplo:

| Dispositivo | MAC | IP reservada |
|---|---|---|
| Impresora | AA:BB:CC:DD:EE:01 | 192.168.10.20 |
| Servidor web | AA:BB:CC:DD:EE:02 | 192.168.40.10 |
| Cámara principal | AA:BB:CC:DD:EE:03 | 192.168.30.20 |

Esto evita configurar manualmente la IP en el dispositivo, pero mantiene una dirección fija.

## IP fija vs reserva DHCP

| Método | Descripción |
|---|---|
| IP fija manual | La IP se configura directamente en el dispositivo |
| Reserva DHCP | El servidor DHCP siempre entrega la misma IP al dispositivo |

En muchos casos, la reserva DHCP es más fácil de administrar porque toda la configuración se controla desde el router o servidor DHCP.

## DNS público y DNS privado

Existen servidores DNS públicos y privados.

Ejemplos de DNS públicos:

```txt
8.8.8.8
1.1.1.1
9.9.9.9
```

Ejemplo de DNS privado o local:

```txt
192.168.10.1
192.168.40.10
```

Un DNS local puede resolver nombres internos como:

```txt
servidor-web.local
impresora.local
```

Y también reenviar consultas externas hacia DNS públicos.

## DNS y seguridad

DNS también es importante para la seguridad.

Un DNS mal configurado puede causar problemas como:

- No poder navegar.
- Resolver nombres incorrectos.
- Enviar tráfico a servidores no deseados.
- Dificultar el acceso a servicios internos.
- Permitir consultas DNS desde redes no autorizadas.

En redes segmentadas, puede ser conveniente definir qué VLANs o subredes pueden usar el DNS interno.

## Errores comunes

Algunos errores frecuentes son:

- Configurar mal el gateway.
- Usar una máscara incorrecta.
- Tener dos servidores DHCP activos en la misma red sin control.
- Entregar direcciones IP que ya están reservadas.
- No separar rangos DHCP por segmento.
- Configurar DNS incorrecto.
- No documentar reservas DHCP.
- No saber qué equipo está entregando DHCP.

## Buenas prácticas

Al configurar DHCP y DNS se recomienda:

- Definir un rango DHCP claro.
- Reservar direcciones para equipos importantes.
- Documentar gateway, DNS y rangos por segmento.
- Evitar que el DHCP entregue direcciones usadas manualmente.
- Usar reservas DHCP para impresoras, servidores o cámaras.
- Mantener separado el DHCP de cada VLAN o subred.
- Revisar que los dispositivos reciban gateway y DNS correctos.
- Documentar nombres internos importantes.

## Ejemplo para este proyecto

| Segmento | Red | Gateway | DHCP | DNS |
|---|---|---|---|---|
| Red principal | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.100-199 | 192.168.10.1 |
| Red invitados | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.100-199 | 192.168.20.1 |
| Red IoT | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.100-199 | 192.168.30.1 |
| Red servidores | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.100-199 | 192.168.40.1 |

Servidor web local:

```txt
Nombre: servidor-web.local
IP:     192.168.40.10
```

Impresora:

```txt
Nombre: impresora.local
IP:     192.168.10.20
```

## Relación con VLANs y subredes

Cada VLAN o subred debe tener una configuración propia de DHCP.

Ejemplo:

```txt
VLAN 10 -> 192.168.10.0/24 -> DHCP 192.168.10.100-199
VLAN 20 -> 192.168.20.0/24 -> DHCP 192.168.20.100-199
VLAN 30 -> 192.168.30.0/24 -> DHCP 192.168.30.100-199
VLAN 40 -> 192.168.40.0/24 -> DHCP 192.168.40.100-199
```

DNS puede ser entregado por el router, firewall o servidor local.

## Conclusión

DHCP permite que los dispositivos reciban configuración de red automáticamente. DNS permite traducir nombres a direcciones IP.

Ambos servicios son fundamentales para que una red sea fácil de usar, administrar y documentar.

En redes segmentadas, DHCP y DNS deben planearse por cada segmento para evitar conflictos, mejorar la administración y facilitar el acceso a servicios internos.