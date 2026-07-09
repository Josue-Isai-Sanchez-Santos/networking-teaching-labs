# Respuestas del Laboratorio 02

## Sección 1: Conversión decimal a binario

### Ejercicio 1

```txt
192.168.10.25
=
11000000.10101000.00001010.00011001
```

### Ejercicio 2

```txt
192.168.20.100
=
11000000.10101000.00010100.01100100
```

### Ejercicio 3

```txt
10.0.0.1
=
00001010.00000000.00000000.00000001
```

### Ejercicio 4

```txt
172.16.5.200
=
10101100.00010000.00000101.11001000
```

## Sección 2: Conversión binario a decimal

### Ejercicio 5

```txt
11000000 = 192
```

### Ejercicio 6

```txt
10101000 = 168
```

### Ejercicio 7

```txt
00001010 = 10
```

### Ejercicio 8

```txt
11111111 = 255
```

### Ejercicio 9

```txt
10000000 = 128
```

## Sección 3: CIDR y máscaras

| CIDR | Máscara decimal | Bits de host | Hosts utilizables |
|---|---|---:|---:|
| /24 | 255.255.255.0 | 8 | 254 |
| /25 | 255.255.255.128 | 7 | 126 |
| /26 | 255.255.255.192 | 6 | 62 |
| /27 | 255.255.255.224 | 5 | 30 |
| /28 | 255.255.255.240 | 4 | 14 |
| /29 | 255.255.255.248 | 3 | 6 |
| /30 | 255.255.255.252 | 2 | 2 |

## Sección 4: Identificación de red, hosts y broadcast

### Ejercicio 10

```txt
192.168.10.0/24
```

| Dato | Respuesta |
|---|---|
| Máscara decimal | 255.255.255.0 |
| Dirección de red | 192.168.10.0 |
| Primer host utilizable | 192.168.10.1 |
| Último host utilizable | 192.168.10.254 |
| Broadcast | 192.168.10.255 |
| Hosts utilizables | 254 |

### Ejercicio 11

```txt
192.168.20.0/24
```

| Dato | Respuesta |
|---|---|
| Máscara decimal | 255.255.255.0 |
| Dirección de red | 192.168.20.0 |
| Primer host utilizable | 192.168.20.1 |
| Último host utilizable | 192.168.20.254 |
| Broadcast | 192.168.20.255 |
| Hosts utilizables | 254 |

### Ejercicio 12

```txt
192.168.10.0/25
```

| Dato | Respuesta |
|---|---|
| Máscara decimal | 255.255.255.128 |
| Dirección de red | 192.168.10.0 |
| Primer host utilizable | 192.168.10.1 |
| Último host utilizable | 192.168.10.126 |
| Broadcast | 192.168.10.127 |
| Hosts utilizables | 126 |

### Ejercicio 13

```txt
192.168.10.128/25
```

| Dato | Respuesta |
|---|---|
| Máscara decimal | 255.255.255.128 |
| Dirección de red | 192.168.10.128 |
| Primer host utilizable | 192.168.10.129 |
| Último host utilizable | 192.168.10.254 |
| Broadcast | 192.168.10.255 |
| Hosts utilizables | 126 |

## Sección 5: División de una red /24 en subredes /26

Red original:

```txt
192.168.10.0/24
```

Nueva máscara:

```txt
/26 = 255.255.255.192
```

Bits prestados:

```txt
/26 - /24 = 2 bits
```

Cantidad de subredes:

```txt
2^2 = 4 subredes
```

Bits de host:

```txt
32 - 26 = 6 bits de host
```

Hosts por subred:

```txt
2^6 - 2 = 62 hosts utilizables
```

Tamaño de bloque:

```txt
256 - 192 = 64
```

Subredes:

| Subred | Dirección de red | Primer host | Último host | Broadcast | Hosts utilizables |
|---|---|---|---|---|---:|
| 1 | 192.168.10.0/26 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 | 62 |
| 2 | 192.168.10.64/26 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 | 62 |
| 3 | 192.168.10.128/26 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 | 62 |
| 4 | 192.168.10.192/26 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 | 62 |

## Sección 6: Asignación de subredes

| Segmento | Subred asignada | Justificación |
|---|---|---|
| Red principal | 192.168.10.0/26 | Contiene dispositivos confiables y requiere mayor prioridad administrativa |
| Red de invitados | 192.168.10.64/26 | Separa dispositivos temporales del resto de la red |
| Red IoT | 192.168.10.128/26 | Aísla dispositivos inteligentes con menor nivel de confianza |
| Red de servidores | 192.168.10.192/26 | Separa servicios internos para aplicar reglas específicas |

## Sección 7: Preguntas de análisis

### 1. ¿Por qué una red /24 tiene 254 hosts utilizables y no 256?

Porque una red `/24` tiene 256 direcciones totales, pero la primera se reserva como dirección de red y la última como dirección de broadcast.

```txt
256 - 2 = 254
```

### 2. ¿Qué representa la dirección de red?

Representa a toda la red o segmento. No identifica a un dispositivo individual.

### 3. ¿Qué representa la dirección de broadcast?

Representa una dirección especial usada para enviar tráfico a todos los dispositivos de la misma red.

### 4. ¿Qué diferencia hay entre /24 y /26?

Una red `/24` tiene 254 hosts utilizables.

Una red `/26` tiene 62 hosts utilizables.

`/26` es más pequeña que `/24`.

### 5. ¿Cuál red permite más hosts, /23 o /24?

Permite más hosts `/23`.

```txt
/23 = 510 hosts utilizables
/24 = 254 hosts utilizables
```

`/23` tiene más bits disponibles para hosts.

### 6. ¿Por qué no conviene colocar invitados, IoT y computadoras personales en la misma red?

Porque todos podrían intentar comunicarse entre sí. Eso aumenta el riesgo si un dispositivo invitado o IoT está comprometido.

### 7. ¿El subnetting por sí solo bloquea la comunicación entre redes?

No. El subnetting separa rangos de red, pero para bloquear o permitir tráfico se necesitan reglas de firewall, ACLs o configuración de router.

### 8. ¿Qué otro componente se necesita para controlar el tráfico entre segmentos?

Se necesita un firewall, router con reglas de acceso o listas de control de acceso.

### 9. ¿Por qué es importante documentar los rangos IP?

Porque ayuda a administrar la red, evitar conflictos de IP, localizar dispositivos y diagnosticar problemas.

### 10. ¿Qué ventaja tiene dejar espacio libre para crecimiento en una red?

Permite agregar nuevos dispositivos en el futuro sin rediseñar toda la red.