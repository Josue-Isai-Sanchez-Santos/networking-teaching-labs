# Ejercicios del Laboratorio 02

## Sección 1: Conversión decimal a binario

Convierte las siguientes direcciones IP a binario.

### Ejercicio 1

```txt
192.168.10.25
```

### Ejercicio 2

```txt
192.168.20.100
```

### Ejercicio 3

```txt
10.0.0.1
```

### Ejercicio 4

```txt
172.16.5.200
```

## Sección 2: Conversión binario a decimal

Convierte los siguientes octetos binarios a decimal.

### Ejercicio 5

```txt
11000000
```

### Ejercicio 6

```txt
10101000
```

### Ejercicio 7

```txt
00001010
```

### Ejercicio 8

```txt
11111111
```

### Ejercicio 9

```txt
10000000
```

## Sección 3: CIDR y máscaras

Completa la tabla.

| CIDR | Máscara decimal | Bits de host | Hosts utilizables |
|---|---|---:|---:|
| /24 |  |  |  |
| /25 |  |  |  |
| /26 |  |  |  |
| /27 |  |  |  |
| /28 |  |  |  |
| /29 |  |  |  |
| /30 |  |  |  |

## Sección 4: Identificación de red, hosts y broadcast

Completa los datos para cada red.

### Ejercicio 10

```txt
192.168.10.0/24
```

| Dato | Respuesta |
|---|---|
| Máscara decimal |  |
| Dirección de red |  |
| Primer host utilizable |  |
| Último host utilizable |  |
| Broadcast |  |
| Hosts utilizables |  |

### Ejercicio 11

```txt
192.168.20.0/24
```

| Dato | Respuesta |
|---|---|
| Máscara decimal |  |
| Dirección de red |  |
| Primer host utilizable |  |
| Último host utilizable |  |
| Broadcast |  |
| Hosts utilizables |  |

### Ejercicio 12

```txt
192.168.10.0/25
```

| Dato | Respuesta |
|---|---|
| Máscara decimal |  |
| Dirección de red |  |
| Primer host utilizable |  |
| Último host utilizable |  |
| Broadcast |  |
| Hosts utilizables |  |

### Ejercicio 13

```txt
192.168.10.128/25
```

| Dato | Respuesta |
|---|---|
| Máscara decimal |  |
| Dirección de red |  |
| Primer host utilizable |  |
| Último host utilizable |  |
| Broadcast |  |
| Hosts utilizables |  |

## Sección 5: División de una red /24 en subredes /26

Divide la siguiente red en cuatro subredes `/26`:

```txt
192.168.10.0/24
```

Completa la tabla.

| Subred | Dirección de red | Primer host | Último host | Broadcast | Hosts utilizables |
|---|---|---|---|---|---:|
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |
| 4 |  |  |  |  |  |

## Sección 6: Asignación de subredes

Usando las cuatro subredes `/26`, asigna una subred a cada segmento.

| Segmento | Subred asignada | Justificación |
|---|---|---|
| Red principal |  |  |
| Red de invitados |  |  |
| Red IoT |  |  |
| Red de servidores |  |  |

## Sección 7: Preguntas de análisis

1. ¿Por qué una red `/24` tiene 254 hosts utilizables y no 256?

2. ¿Qué representa la dirección de red?

3. ¿Qué representa la dirección de broadcast?

4. ¿Qué diferencia hay entre `/24` y `/26`?

5. ¿Cuál red permite más hosts, `/23` o `/24`? Explica por qué.

6. ¿Por qué no conviene colocar invitados, IoT y computadoras personales en la misma red?

7. ¿El subnetting por sí solo bloquea la comunicación entre redes? Justifica tu respuesta.

8. ¿Qué otro componente se necesita para controlar el tráfico entre segmentos?

9. ¿Por qué es importante documentar los rangos IP?

10. ¿Qué ventaja tiene dejar espacio libre para crecimiento en una red?