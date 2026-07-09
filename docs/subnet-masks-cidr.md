# Máscaras de subred y notación CIDR

## Introducción

Una máscara de subred permite separar una dirección IP en dos partes:

```txt
Parte de red + Parte de host
```

La parte de red indica a qué red pertenece una dirección.

La parte de host identifica a un dispositivo específico dentro de esa red.

Para entender subredes, es necesario comprender las máscaras de subred y la notación CIDR.

## ¿Qué es una máscara de subred?

Una máscara de subred es un valor de 32 bits que indica qué parte de una dirección IP corresponde a la red y qué parte corresponde a los hosts.

Ejemplo:

```txt
IP:       192.168.10.25
Máscara:  255.255.255.0
```

La máscara también puede escribirse en formato CIDR:

```txt
192.168.10.25/24
```

Ambas formas indican lo mismo:

```txt
255.255.255.0 = /24
```

## ¿Qué significa /24?

La notación `/24` significa que los primeros 24 bits de la dirección IP pertenecen a la red.

Una dirección IPv4 tiene 32 bits en total.

Entonces:

```txt
32 bits totales - 24 bits de red = 8 bits de host
```

Eso significa que quedan 8 bits para direcciones de dispositivos.

## Máscara /24 en binario

La máscara `/24` se representa así:

```txt
11111111.11111111.11111111.00000000
```

Los bits en `1` representan la parte de red.

Los bits en `0` representan la parte de host.

En decimal:

```txt
11111111 = 255
11111111 = 255
11111111 = 255
00000000 = 0
```

Resultado:

```txt
/24 = 255.255.255.0
```

## Ejemplo con 192.168.10.25/24

Dirección IP:

```txt
192.168.10.25
```

Máscara:

```txt
255.255.255.0
```

CIDR:

```txt
/24
```

Esto significa que la red es:

```txt
192.168.10.0
```

Y el dispositivo es el host:

```txt
25
```

La red completa sería:

```txt
192.168.10.0/24
```

## Dirección de red

La dirección de red identifica a toda la red.

No se asigna a un dispositivo porque representa al segmento completo.

Ejemplo:

```txt
192.168.10.0/24
```

En esta red, la dirección:

```txt
192.168.10.0
```

representa a toda la red.

Por eso no se asigna a una computadora, celular, impresora o servidor.

## Dirección de broadcast

La dirección de broadcast sirve para enviar un mensaje a todos los dispositivos dentro de la misma red.

Ejemplo:

```txt
192.168.10.255
```

En una red `/24`, normalmente la última dirección es el broadcast.

Por eso tampoco se asigna a un dispositivo.

## ¿Por qué no se usa la primera y la última IP?

En redes IPv4 tradicionales:

```txt
Primera dirección = Dirección de red
Última dirección  = Dirección de broadcast
```

Ejemplo:

```txt
Red: 192.168.10.0/24
```

| Dirección | Uso |
|---|---|
| 192.168.10.0 | Dirección de red |
| 192.168.10.1 | Primer host utilizable |
| 192.168.10.2 | Host utilizable |
| ... | ... |
| 192.168.10.254 | Último host utilizable |
| 192.168.10.255 | Broadcast |

Por eso una red con 256 direcciones totales no tiene 256 hosts utilizables, sino 254.

## Fórmula para calcular hosts

La fórmula es:

```txt
Hosts utilizables = 2^(bits de host) - 2
```

Se resta 2 porque:

```txt
1 dirección se reserva para la red
1 dirección se reserva para broadcast
```

## Ejemplo con /24

```txt
/24
```

IPv4 tiene 32 bits.

```txt
32 - 24 = 8 bits de host
```

Cálculo:

```txt
2^8 = 256 direcciones totales
256 - 2 = 254 hosts utilizables
```

Resultado:

```txt
/24 permite 254 hosts utilizables
```

## Ejemplo con /23

```txt
/23
```

Cálculo:

```txt
32 - 23 = 9 bits de host
2^9 = 512 direcciones totales
512 - 2 = 510 hosts utilizables
```

Resultado:

```txt
/23 permite 510 hosts utilizables
```

Una red `/23` es más grande que una red `/24`.

Ejemplo:

```txt
192.168.10.0/23
```

Rango:

```txt
Dirección de red:      192.168.10.0
Primer host usable:    192.168.10.1
Último host usable:    192.168.11.254
Broadcast:             192.168.11.255
```

Observa que un `/23` abarca dos bloques de `/24`:

```txt
192.168.10.x
192.168.11.x
```

## Ejemplo con /25

```txt
/25
```

Cálculo:

```txt
32 - 25 = 7 bits de host
2^7 = 128 direcciones totales
128 - 2 = 126 hosts utilizables
```

Un `/25` divide un `/24` en dos subredes:

```txt
192.168.10.0/25
192.168.10.128/25
```

Primera subred:

```txt
Red:          192.168.10.0
Primer host:  192.168.10.1
Último host:  192.168.10.126
Broadcast:    192.168.10.127
```

Segunda subred:

```txt
Red:          192.168.10.128
Primer host:  192.168.10.129
Último host:  192.168.10.254
Broadcast:    192.168.10.255
```

## Tabla de máscaras comunes

| CIDR | Máscara decimal | Bits de host | Direcciones totales | Hosts utilizables |
|---:|---|---:|---:|---:|
| /16 | 255.255.0.0 | 16 | 65536 | 65534 |
| /17 | 255.255.128.0 | 15 | 32768 | 32766 |
| /18 | 255.255.192.0 | 14 | 16384 | 16382 |
| /19 | 255.255.224.0 | 13 | 8192 | 8190 |
| /20 | 255.255.240.0 | 12 | 4096 | 4094 |
| /21 | 255.255.248.0 | 11 | 2048 | 2046 |
| /22 | 255.255.252.0 | 10 | 1024 | 1022 |
| /23 | 255.255.254.0 | 9 | 512 | 510 |
| /24 | 255.255.255.0 | 8 | 256 | 254 |
| /25 | 255.255.255.128 | 7 | 128 | 126 |
| /26 | 255.255.255.192 | 6 | 64 | 62 |
| /27 | 255.255.255.224 | 5 | 32 | 30 |
| /28 | 255.255.255.240 | 4 | 16 | 14 |
| /29 | 255.255.255.248 | 3 | 8 | 6 |
| /30 | 255.255.255.252 | 2 | 4 | 2 |

## Tamaño de bloque

El tamaño de bloque indica cada cuántas direcciones empieza una nueva subred.

Se calcula con esta fórmula:

```txt
Tamaño de bloque = 256 - valor de la máscara en el octeto interesante
```

Ejemplo con `/26`:

```txt
Máscara: 255.255.255.192
Octeto interesante: 192

256 - 192 = 64
```

Entonces las subredes avanzan de 64 en 64:

```txt
192.168.10.0/26
192.168.10.64/26
192.168.10.128/26
192.168.10.192/26
```

## Ejemplo con /26

Una red `/26` tiene:

```txt
32 - 26 = 6 bits de host
2^6 = 64 direcciones
64 - 2 = 62 hosts utilizables
```

Subredes dentro de `192.168.10.0/24`:

| Subred | Dirección de red | Primer host | Último host | Broadcast |
|---|---|---|---|---|
| 1 | 192.168.10.0 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| 2 | 192.168.10.64 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| 4 | 192.168.10.192 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

## ¿Cómo elegir una máscara?

La máscara se elige según la cantidad de dispositivos que necesita la red.

Ejemplo:

| Necesidad | Máscara recomendada | Hosts utilizables |
|---|---|---:|
| Hasta 2 hosts | /30 | 2 |
| Hasta 6 hosts | /29 | 6 |
| Hasta 14 hosts | /28 | 14 |
| Hasta 30 hosts | /27 | 30 |
| Hasta 62 hosts | /26 | 62 |
| Hasta 126 hosts | /25 | 126 |
| Hasta 254 hosts | /24 | 254 |
| Hasta 510 hosts | /23 | 510 |

Siempre conviene dejar espacio para crecimiento.

Por ejemplo, si hoy necesitas 20 dispositivos, no conviene usar una red de 20 exactos, porque las redes no crecen de uno en uno. Se elige la máscara que soporte esa cantidad.

Para 20 dispositivos:

```txt
/27 permite 30 hosts utilizables
```

Entonces `/27` sería una opción adecuada.

## Relación entre CIDR y seguridad

La máscara no es una medida de seguridad por sí sola. Una máscara solo define el tamaño de una red.

La seguridad se logra combinando:

- Segmentación.
- VLANs.
- Firewall.
- Buenas contraseñas.
- Control de acceso.
- Actualizaciones.
- Monitoreo.

Por ejemplo, una red de invitados puede usar `/24`, pero si no hay reglas de firewall, los invitados podrían intentar acceder a otros segmentos.

## Conclusión

Las máscaras de subred y la notación CIDR permiten definir el tamaño de una red. La máscara indica qué parte de una IP pertenece a la red y qué parte pertenece a los hosts.

Comprender `/24`, `/23`, `/25` y otros prefijos permite calcular rangos, hosts disponibles, dirección de red y broadcast.