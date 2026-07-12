# Laboratorio 03: DNS y DHCP

## Tema

Asignación automática de direcciones IP mediante DHCP y resolución de nombres mediante DNS.

## Objetivo

Comprender cómo DHCP asigna configuración de red a los dispositivos y cómo DNS permite resolver nombres hacia direcciones IP dentro de una red local.

## Aprendizajes esperados

Al finalizar este laboratorio, el estudiante será capaz de:

- Explicar qué es DHCP.
- Explicar qué es DNS.
- Identificar los datos que entrega un servidor DHCP.
- Diseñar rangos DHCP por segmento de red.
- Diferenciar entre IP fija y reserva DHCP.
- Relacionar nombres internos con direcciones IP.
- Documentar configuraciones básicas de red.

## Documentos de apoyo

Antes de realizar este laboratorio, se recomienda revisar:

```txt
docs/ip-addressing-binary.md
docs/subnet-masks-cidr.md
docs/subnetting-guide.md
docs/vlan-concepts.md
docs/dns-dhcp.md
```

## Escenario

Una pequeña oficina tiene una red segmentada con cuatro áreas:

| Segmento | Red | Gateway |
|---|---|---|
| Red principal | 192.168.10.0/24 | 192.168.10.1 |
| Red de invitados | 192.168.20.0/24 | 192.168.20.1 |
| Red IoT | 192.168.30.0/24 | 192.168.30.1 |
| Red de servidores | 192.168.40.0/24 | 192.168.40.1 |

Se requiere definir rangos DHCP y nombres DNS internos para algunos servicios.

## Parte 1: Diseño de rangos DHCP

El estudiante deberá proponer rangos DHCP para cada segmento.

Ejemplo recomendado:

| Segmento | Red | Gateway | Rango DHCP |
|---|---|---|---|
| Red principal | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.100-199 |
| Red de invitados | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.100-199 |
| Red IoT | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.100-199 |
| Red de servidores | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.100-199 |

## Parte 2: Reservas DHCP

Algunos dispositivos deben recibir siempre la misma IP.

| Dispositivo | Segmento | IP recomendada |
|---|---|---|
| Impresora | Red principal | 192.168.10.20 |
| Servidor web local | Red de servidores | 192.168.40.10 |
| Cámara principal | Red IoT | 192.168.30.20 |
| Switch administrable | Red principal | 192.168.10.10 |

El estudiante deberá explicar por qué estos dispositivos no deberían depender de una IP aleatoria.

## Parte 3: Nombres DNS internos

Se deben proponer nombres internos para servicios locales.

Ejemplo:

| Nombre DNS | IP | Uso |
|---|---|---|
| impresora.local | 192.168.10.20 | Impresora interna |
| servidor-web.local | 192.168.40.10 | Servidor web local |
| camara-principal.local | 192.168.30.20 | Cámara IoT |
| switch.local | 192.168.10.10 | Switch administrable |

## Parte 4: Análisis de configuración recibida

Un dispositivo de la red principal recibe esta configuración:

```txt
IP:        192.168.10.105
Máscara:   255.255.255.0
Gateway:   192.168.10.1
DNS:       192.168.10.1
```

El estudiante deberá identificar:

- A qué red pertenece.
- Si la IP está dentro del rango DHCP.
- Cuál es su gateway.
- Qué servidor DNS está usando.
- Si podría comunicarse con internet.
- Si debería poder acceder al servidor web local.

## Actividades del estudiante

El estudiante deberá:

1. Completar la tabla de rangos DHCP.
2. Definir reservas DHCP para dispositivos importantes.
3. Crear una tabla de nombres DNS internos.
4. Analizar configuraciones de red entregadas a dispositivos.
5. Explicar la diferencia entre DHCP y DNS.
6. Responder las preguntas del archivo `questions.md`.

## Entregables esperados

El estudiante deberá entregar:

- Tabla de rangos DHCP por segmento.
- Tabla de reservas DHCP.
- Tabla de nombres DNS internos.
- Análisis de configuración de al menos tres dispositivos.
- Respuestas a las preguntas de análisis.

## Criterios de evaluación

| Criterio | Excelente | Bueno | Necesita mejorar |
|---|---|---|---|
| Comprensión de DHCP | Explica claramente su función | Explica parcialmente | No identifica su función |
| Comprensión de DNS | Explica claramente su función | Explica parcialmente | No identifica su función |
| Rangos DHCP | Propone rangos correctos y ordenados | Presenta errores menores | Rangos incorrectos o conflictivos |
| Reservas DHCP | Identifica correctamente dispositivos importantes | Omite algunos dispositivos | No justifica reservas |
| Documentación | Presenta tablas claras y completas | Documentación parcial | Documentación incompleta |

## Conclusión

DHCP y DNS son servicios esenciales para la operación de una red. DHCP facilita la asignación automática de configuración IP, mientras que DNS permite usar nombres en lugar de memorizar direcciones IP.

En redes segmentadas, estos servicios deben planearse cuidadosamente para evitar conflictos y mejorar la administración.