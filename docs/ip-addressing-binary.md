# Direcciones IP y sistema binario

## Introducción

Las redes de computadoras utilizan direcciones IP para identificar dispositivos dentro de una red. Aunque normalmente vemos las direcciones IP en formato decimal, internamente las computadoras trabajan con números binarios.

Comprender el sistema binario ayuda a entender temas importantes como:

- Direcciones IPv4.
- Máscaras de subred.
- Notación CIDR.
- Dirección de red.
- Dirección de broadcast.
- Rango de hosts utilizables.
- Subnetting.

Sin esta base, temas como `/24`, `/23`, `255.255.255.0` o `192.168.10.0/24` pueden parecer memorización. En realidad, todo sale de operaciones binarias.

## ¿Qué es una dirección IPv4?

Una dirección IPv4 es un número de 32 bits que identifica a un dispositivo dentro de una red.

Normalmente se escribe en formato decimal separado por puntos:

```txt
192.168.10.25
```

Esa dirección tiene 4 partes. Cada parte se llama **octeto** porque contiene 8 bits.

```txt
192 . 168 . 10 . 25
```

Cada octeto puede tener valores desde 0 hasta 255.

Esto ocurre porque 8 bits pueden representar 256 valores posibles:

```txt
Desde 0 hasta 255
```

## ¿Qué es un bit?

Un bit es la unidad mínima de información en computación.

Un bit solo puede tener dos valores:

```txt
0
1
```

Por eso se llama sistema binario: trabaja con base 2.

## ¿Qué es un octeto?

Un octeto es un grupo de 8 bits.

Ejemplo:

```txt
11000000
```

Una dirección IPv4 tiene 4 octetos:

```txt
Octeto 1   Octeto 2   Octeto 3   Octeto 4
192        168        10         25
```

En binario:

```txt
11000000   10101000   00001010   00011001
```

Por eso una IPv4 tiene 32 bits:

```txt
8 bits + 8 bits + 8 bits + 8 bits = 32 bits
```

## ¿Por qué se usa binario?

Las computadoras no interpretan las direcciones IP como texto normal. Internamente trabajan con bits.

Por ejemplo, cuando una computadora revisa si una IP pertenece a una red, no lo hace mirando solo los números decimales. Lo hace usando operaciones binarias entre:

- La dirección IP.
- La máscara de subred.

Esto permite saber:

- Qué parte de la IP representa la red.
- Qué parte representa al dispositivo o host.
- Cuál es la dirección de red.
- Cuál es la dirección de broadcast.
- Qué direcciones pueden usarse para dispositivos.

## Valores binarios de un octeto

Un octeto tiene 8 posiciones. Cada posición tiene un valor:

```txt
128  64  32  16  8  4  2  1
```

Si un bit está en `1`, se suma su valor.

Si un bit está en `0`, no se suma.

Ejemplo:

```txt
11000000
```

Se calcula así:

```txt
1   1   0   0   0   0   0   0
128 64  32  16  8   4   2   1
```

Se suman solo los valores donde hay `1`:

```txt
128 + 64 = 192
```

Por eso:

```txt
11000000 = 192
```

## Conversión de decimal a binario

Para convertir un número decimal a binario, se puede comparar contra los valores del octeto:

```txt
128 64 32 16 8 4 2 1
```

Ejemplo: convertir `192` a binario.

Primero revisamos si 192 puede usar 128:

```txt
192 - 128 = 64
```

Sí se usa 128, por lo tanto el primer bit es 1.

Luego usamos 64:

```txt
64 - 64 = 0
```

Sí se usa 64, por lo tanto el segundo bit es 1.

Ya no queda nada, los demás bits son 0.

Resultado:

```txt
192 = 11000000
```

## Ejemplo: convertir 168 a binario

Valores del octeto:

```txt
128 64 32 16 8 4 2 1
```

Convertimos 168:

```txt
168 - 128 = 40
40 no alcanza para 64
40 - 32 = 8
8 no alcanza para 16
8 - 8 = 0
```

Entonces:

```txt
128 = 1
64  = 0
32  = 1
16  = 0
8   = 1
4   = 0
2   = 0
1   = 0
```

Resultado:

```txt
168 = 10101000
```

## Ejemplo: convertir 10 a binario

```txt
10 no alcanza para 128
10 no alcanza para 64
10 no alcanza para 32
10 no alcanza para 16
10 - 8 = 2
2 no alcanza para 4
2 - 2 = 0
0 no alcanza para 1
```

Resultado:

```txt
10 = 00001010
```

## Ejemplo: convertir 25 a binario

```txt
25 no alcanza para 128
25 no alcanza para 64
25 no alcanza para 32
25 - 16 = 9
9 - 8 = 1
1 no alcanza para 4
1 no alcanza para 2
1 - 1 = 0
```

Resultado:

```txt
25 = 00011001
```

## Conversión completa de una IP

Dirección decimal:

```txt
192.168.10.25
```

Conversión por octeto:

| Decimal | Binario |
|---:|---|
| 192 | 11000000 |
| 168 | 10101000 |
| 10 | 00001010 |
| 25 | 00011001 |

Resultado:

```txt
192.168.10.25
=
11000000.10101000.00001010.00011001
```

## Conversión de binario a decimal

Para convertir binario a decimal, se suman los valores donde haya `1`.

Ejemplo:

```txt
00011001
```

Valores:

```txt
0   0   0   1   1   0   0   1
128 64  32  16  8   4   2   1
```

Se suman:

```txt
16 + 8 + 1 = 25
```

Entonces:

```txt
00011001 = 25
```

## Tabla de referencia rápida

| Decimal | Binario |
|---:|---|
| 0 | 00000000 |
| 1 | 00000001 |
| 2 | 00000010 |
| 4 | 00000100 |
| 8 | 00001000 |
| 16 | 00010000 |
| 32 | 00100000 |
| 64 | 01000000 |
| 128 | 10000000 |
| 192 | 11000000 |
| 224 | 11100000 |
| 240 | 11110000 |
| 248 | 11111000 |
| 252 | 11111100 |
| 254 | 11111110 |
| 255 | 11111111 |

Esta tabla será útil para entender máscaras de subred.

## Parte de red y parte de host

Una dirección IP se divide en dos partes:

```txt
Parte de red + Parte de host
```

La parte de red identifica a la red.

La parte de host identifica a un dispositivo dentro de esa red.

Ejemplo:

```txt
192.168.10.25/24
```

En este caso, los primeros 24 bits son la parte de red.

La parte restante se usa para hosts.

```txt
32 bits totales - 24 bits de red = 8 bits de host
```

## Ejemplo visual con /24

Dirección:

```txt
192.168.10.25/24
```

En binario:

```txt
IP:
11000000.10101000.00001010.00011001

Máscara /24:
11111111.11111111.11111111.00000000
```

Los bits en `1` de la máscara indican la parte de red.

Los bits en `0` indican la parte de host.

```txt
Red:  11000000.10101000.00001010
Host: 00011001
```

En decimal, la red es:

```txt
192.168.10.0
```

Y el host es:

```txt
25
```

## ¿Por qué esto importa?

Porque para calcular subredes no basta con mirar la IP en decimal. Hay que entender qué bits pertenecen a la red y cuáles pertenecen a los hosts.

Esto permite calcular:

- Dirección de red.
- Dirección de broadcast.
- Primer host utilizable.
- Último host utilizable.
- Cantidad de hosts disponibles.
- Tamaño de cada subred.

## Conclusión

Las direcciones IPv4 se escriben normalmente en decimal, pero internamente se interpretan en binario. Cada dirección IPv4 tiene 32 bits divididos en 4 octetos.

Comprender binario permite entender cómo funcionan las máscaras de subred, la notación CIDR y el proceso de subnetting.