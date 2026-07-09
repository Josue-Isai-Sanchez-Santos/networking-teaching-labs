# Laboratorio 02: Subredes y cálculo de rangos IP

## Tema

Cálculo de subredes, máscaras, rangos de hosts, dirección de red y broadcast.

## Objetivo

Aplicar conceptos de direccionamiento IPv4, sistema binario, máscaras de subred y notación CIDR para calcular rangos de red utilizables en un escenario práctico.

## Aprendizajes esperados

Al finalizar este laboratorio, el estudiante será capaz de:

- Interpretar una dirección IPv4 con notación CIDR.
- Identificar la máscara de subred correspondiente.
- Calcular la cantidad de hosts utilizables.
- Determinar dirección de red y broadcast.
- Identificar primer y último host utilizable.
- Dividir una red `/24` en subredes más pequeñas.
- Relacionar el subnetting con el diseño de redes segmentadas.

## Documentos de apoyo

Antes de realizar este laboratorio, se recomienda revisar:

```txt
docs/ip-addressing-binary.md
docs/subnet-masks-cidr.md
docs/subnetting-guide.md
```

## Escenario

Una pequeña oficina desea organizar su red interna en varios segmentos:

- Red principal.
- Red de invitados.
- Red IoT.
- Red de servidores.

Para la primera versión del diseño se usará un modelo simple con redes `/24`.

Después se realizará un ejercicio más técnico dividiendo una sola red `/24` en cuatro subredes `/26`.

## Parte 1: Diseño simple con redes /24

Segmentos propuestos:

| Segmento | Red |
|---|---|
| Red principal | 192.168.10.0/24 |
| Red de invitados | 192.168.20.0/24 |
| Red IoT | 192.168.30.0/24 |
| Red de servidores | 192.168.40.0/24 |

El estudiante deberá calcular para cada segmento:

- Máscara decimal.
- Dirección de red.
- Primer host utilizable.
- Último host utilizable.
- Dirección de broadcast.
- Cantidad de hosts utilizables.

## Parte 2: División de una red /24 en cuatro subredes

Red original:

```txt
192.168.10.0/24
```

Objetivo:

Dividir la red en cuatro subredes del mismo tamaño.

Para obtener cuatro subredes iguales se utiliza:

```txt
/26
```

Porque:

```txt
/24 -> red original
/26 -> se toman 2 bits adicionales para subredes

2^2 = 4 subredes
```

Cada subred `/26` tiene:

```txt
32 - 26 = 6 bits de host
2^6 = 64 direcciones totales
64 - 2 = 62 hosts utilizables
```

## Subredes esperadas

| Subred | Dirección de red | Primer host | Último host | Broadcast |
|---|---|---|---|---|
| 1 | 192.168.10.0/26 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| 2 | 192.168.10.64/26 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128/26 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| 4 | 192.168.10.192/26 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

## Asignación sugerida

| Segmento | Subred asignada |
|---|---|
| Red principal | 192.168.10.0/26 |
| Red de invitados | 192.168.10.64/26 |
| Red IoT | 192.168.10.128/26 |
| Red de servidores | 192.168.10.192/26 |

## Actividades del estudiante

El estudiante deberá:

1. Completar los ejercicios del archivo `exercises.md`.
2. Convertir al menos tres direcciones IP de decimal a binario.
3. Identificar la máscara decimal de diferentes prefijos CIDR.
4. Calcular hosts utilizables para `/24`, `/25`, `/26`, `/27` y `/28`.
5. Calcular los rangos de subredes para `192.168.10.0/24` dividido en `/26`.
6. Asignar cada subred a un segmento de red.
7. Justificar por qué esa división es útil para una red doméstica o de pequeña oficina.

## Entregables esperados

El estudiante deberá entregar:

- Ejercicios resueltos.
- Tabla de subredes completa.
- Explicación breve del procedimiento utilizado.
- Asignación de segmentos.
- Conclusión personal sobre la utilidad del subnetting.

## Criterios de evaluación

| Criterio | Excelente | Bueno | Necesita mejorar |
|---|---|---|---|
| Conversión binaria | Convierte correctamente las direcciones | Presenta pocos errores | No demuestra comprensión |
| Identificación de máscaras | Relaciona CIDR y máscara correctamente | Presenta algunos errores | No identifica las máscaras |
| Cálculo de hosts | Calcula correctamente hosts utilizables | Presenta errores menores | No aplica la fórmula |
| Rangos de subred | Calcula red, hosts y broadcast correctamente | Presenta errores parciales | Los rangos son incorrectos |
| Justificación | Explica claramente la utilidad del subnetting | Explica parcialmente | No justifica técnicamente |

## Conclusión

El subnetting permite dividir una red en segmentos más pequeños y organizados. Comprender máscaras, CIDR, red, broadcast y hosts utilizables es fundamental para diseñar redes más seguras y administrables.