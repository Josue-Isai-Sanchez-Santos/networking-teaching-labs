# Guía de subnetting

## Introducción

El subnetting es el proceso de dividir una red grande en redes más pequeñas.

Esto permite organizar mejor los dispositivos, reducir riesgos y controlar la comunicación entre segmentos.

En este proyecto, el subnetting se utiliza para diseñar redes separadas para:

- Dispositivos principales.
- Invitados.
- Dispositivos IoT.
- Servidores internos.

## ¿Qué problema resuelve el subnetting?

Supongamos que una pequeña oficina conecta todos sus dispositivos a una sola red:

```txt
192.168.10.0/24
```

En esa red podrían estar:

- Computadoras personales.
- Teléfonos.
- Cámaras.
- Smart TV.
- Impresoras.
- Servidores.
- Dispositivos de invitados.

El problema es que todos estarían dentro del mismo segmento. Si no hay separación, un dispositivo invitado o un equipo IoT podría intentar comunicarse con computadoras personales o servidores internos.

El subnetting permite dividir la red en partes más pequeñas.

## Ejemplo sin segmentación

```txt
Red única: 192.168.10.0/24
```

Todos los dispositivos están juntos:

```txt
Computadoras
Teléfonos
Invitados
IoT
Servidor web
Impresora
```

Esto es simple, pero no es lo más seguro ni lo más ordenado.

## Ejemplo con segmentación

```txt
Red principal:      192.168.10.0/24
Red de invitados:   192.168.20.0/24
Red IoT:            192.168.30.0/24
Red de servidores:  192.168.40.0/24
```

Ahora los dispositivos se organizan por función.

Cada red puede tener sus propias reglas.

## Caso realista: proveedor de internet y NAT

En una casa u oficina pequeña, el proveedor de internet normalmente entrega una sola conexión al módem u ONT.

Esa conexión puede tener:

- Una IP pública dinámica.
- Una IP pública fija.
- Una IP privada si el proveedor usa CGNAT.

Esa IP pertenece al lado WAN del router.

La segmentación se realiza dentro de la red local, usando direcciones privadas.

Ejemplo:

```txt
Internet
   |
Proveedor de internet
   |
Módem / ONT
   |
Router / Firewall con NAT
   |
------------------------------------------------
|              |              |                |
Red principal  Red invitados  Red IoT          Red servidores
```

Todos los segmentos internos pueden salir a internet usando la misma conexión del proveedor mediante NAT.

## Direcciones privadas usadas en redes locales

Para redes internas normalmente se usan direcciones privadas.

Rangos privados comunes:

| Rango privado | Uso común |
|---|---|
| 10.0.0.0/8 | Redes grandes |
| 172.16.0.0/12 | Redes medianas |
| 192.168.0.0/16 | Redes domésticas y pequeñas oficinas |

En este proyecto usaremos el rango:

```txt
192.168.0.0/16
```

De ahí tomaremos redes como:

```txt
192.168.10.0/24
192.168.20.0/24
192.168.30.0/24
192.168.40.0/24
```

## Método para hacer subnetting

Para hacer subnetting de forma ordenada, se pueden seguir estos pasos:

1. Identificar cuántas redes se necesitan.
2. Identificar cuántos hosts necesita cada red.
3. Elegir una máscara adecuada para cada red.
4. Asignar rangos de IP.
5. Definir puerta de enlace para cada red.
6. Reservar direcciones importantes.
7. Documentar el diseño.
8. Definir reglas de comunicación.

## Paso 1: Identificar redes necesarias

Para el escenario base se necesitan cuatro segmentos:

| Segmento | Propósito |
|---|---|
| Red principal | Dispositivos confiables |
| Red de invitados | Visitantes |
| Red IoT | Dispositivos inteligentes |
| Red de servidores | Servicios internos |

## Paso 2: Estimar cantidad de hosts

Ejemplo:

| Segmento | Dispositivos actuales | Crecimiento estimado |
|---|---:|---:|
| Red principal | 5 | Hasta 50 |
| Red de invitados | Variable | Hasta 50 |
| Red IoT | 5 | Hasta 30 |
| Red de servidores | 1 | Hasta 20 |

No conviene diseñar una red solo para los dispositivos actuales. Siempre se debe considerar crecimiento.

## Paso 3: Elegir máscara

Según la cantidad de hosts:

| Segmento | Hosts estimados | Máscara sugerida | Hosts utilizables |
|---|---:|---|---:|
| Red principal | 50 | /26 | 62 |
| Red de invitados | 50 | /26 | 62 |
| Red IoT | 30 | /27 | 30 |
| Red de servidores | 20 | /27 | 30 |

Este diseño es más ajustado y técnico.

Sin embargo, para una versión introductoria también se puede usar `/24` en cada segmento para facilitar la comprensión:

| Segmento | Red | Hosts utilizables |
|---|---|---:|
| Red principal | 192.168.10.0/24 | 254 |
| Red de invitados | 192.168.20.0/24 | 254 |
| Red IoT | 192.168.30.0/24 | 254 |
| Red de servidores | 192.168.40.0/24 | 254 |

Este segundo diseño desperdicia direcciones, pero es más fácil para estudiantes principiantes.

## Enfoque didáctico del proyecto

Para la versión 1.0 se utilizarán redes `/24` separadas porque son fáciles de entender:

```txt
192.168.10.0/24
192.168.20.0/24
192.168.30.0/24
192.168.40.0/24
```

Más adelante se puede hacer una versión avanzada usando subredes más ajustadas como `/26` y `/27`.

## Paso 4: Asignar rangos de IP

Diseño base:

| Segmento | Red | Primer host | Último host | Broadcast |
|---|---|---|---|---|
| Red principal | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.254 | 192.168.10.255 |
| Red de invitados | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.254 | 192.168.20.255 |
| Red IoT | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.254 | 192.168.30.255 |
| Red de servidores | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.254 | 192.168.40.255 |

## Paso 5: Definir puerta de enlace

La puerta de enlace es la dirección del router o firewall dentro de cada segmento.

Ejemplo:

| Segmento | Puerta de enlace |
|---|---|
| Red principal | 192.168.10.1 |
| Red de invitados | 192.168.20.1 |
| Red IoT | 192.168.30.1 |
| Red de servidores | 192.168.40.1 |

Los dispositivos de cada segmento usan su propia puerta de enlace para comunicarse fuera de su red.

## Paso 6: Reservar direcciones

Una buena práctica es reservar rangos para ciertos usos.

Ejemplo para cada red `/24`:

| Rango | Uso sugerido |
|---|---|
| .1 | Puerta de enlace |
| .2 - .19 | Equipos de red o infraestructura |
| .20 - .99 | Dispositivos con IP fija |
| .100 - .199 | DHCP |
| .200 - .239 | Reservas especiales |
| .240 - .254 | Administración o pruebas |

Ejemplo en la red principal:

| Dirección | Uso |
|---|---|
| 192.168.10.1 | Router / puerta de enlace |
| 192.168.10.10 | Switch administrable |
| 192.168.10.20 | Computadora principal |
| 192.168.10.100 - 192.168.10.199 | Rango DHCP |

## Paso 7: Documentar la red

La documentación debe incluir:

- Nombre del segmento.
- Dirección de red.
- Máscara.
- Puerta de enlace.
- Rango DHCP.
- Dispositivos principales.
- Reglas de firewall.
- Observaciones.

Ejemplo:

| Segmento | Red | Máscara | Gateway | DHCP |
|---|---|---|---|---|
| Red principal | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1 | 192.168.10.100-199 |
| Red invitados | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1 | 192.168.20.100-199 |
| Red IoT | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1 | 192.168.30.100-199 |
| Red servidores | 192.168.40.0/24 | 255.255.255.0 | 192.168.40.1 | 192.168.40.100-199 |

## Paso 8: Definir reglas de comunicación

El subnetting por sí solo no bloquea tráfico. Para controlar la comunicación entre redes se necesitan reglas de firewall o listas de control de acceso.

Ejemplo:

| Origen | Destino | Acción | Razón |
|---|---|---|---|
| Red principal | Internet | Permitir | Usuarios confiables necesitan internet |
| Red principal | Red de servidores | Permitir | Usuarios confiables acceden a servicios internos |
| Red invitados | Internet | Permitir | Invitados solo necesitan navegación |
| Red invitados | Red principal | Bloquear | Proteger dispositivos personales |
| Red invitados | Red servidores | Bloquear | Proteger servicios internos |
| Red IoT | Internet | Permitir | Algunos IoT requieren conexión externa |
| Red IoT | Red principal | Bloquear | Evitar acceso a equipos personales |
| Internet | Redes internas | Bloquear | Evitar accesos externos no autorizados |

## Ejemplo avanzado: usar una sola red /24 y dividirla

Si se quiere trabajar con subnetting real dentro de una sola red `/24`, se puede partir:

```txt
Red original: 192.168.10.0/24
```

Dividir en cuatro subredes `/26`:

| Subred | Red | Primer host | Último host | Broadcast | Hosts |
|---|---|---|---|---|---:|
| 1 | 192.168.10.0/26 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 | 62 |
| 2 | 192.168.10.64/26 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 | 62 |
| 3 | 192.168.10.128/26 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 | 62 |
| 4 | 192.168.10.192/26 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 | 62 |

Asignación posible:

| Segmento | Subred |
|---|---|
| Red principal | 192.168.10.0/26 |
| Red de invitados | 192.168.10.64/26 |
| Red IoT | 192.168.10.128/26 |
| Red de servidores | 192.168.10.192/26 |

Este ejemplo es más técnico porque todas las subredes salen de un mismo bloque inicial.

## Diferencia entre diseño simple y diseño ajustado

Diseño simple:

```txt
192.168.10.0/24
192.168.20.0/24
192.168.30.0/24
192.168.40.0/24
```

Ventajas:

- Fácil de leer.
- Fácil de enseñar.
- Fácil de documentar.
- Útil para principiantes.

Desventajas:

- Desperdicia direcciones.
- No practica tanto el cálculo de subnetting.

Diseño ajustado:

```txt
192.168.10.0/26
192.168.10.64/26
192.168.10.128/26
192.168.10.192/26
```

Ventajas:

- Más técnico.
- Usa mejor el espacio IP.
- Refuerza cálculo de subredes.

Desventajas:

- Más difícil para principiantes.
- Requiere entender binario, máscara y tamaño de bloque.

## Recomendación didáctica

Para estudiantes principiantes:

1. Primero explicar IP y binario.
2. Luego explicar máscaras y CIDR.
3. Después practicar `/24`, `/25`, `/26`.
4. Finalmente diseñar una red segmentada.

Por eso este proyecto incluye documentos separados antes de la práctica.

## Conclusión

El subnetting permite dividir redes grandes en redes más pequeñas. Esto mejora la organización, facilita la administración y permite aplicar reglas de seguridad entre segmentos.

En el escenario base, se usará primero un diseño simple con redes `/24`. Después, en ejercicios más avanzados, se mostrará cómo dividir una red `/24` en subredes `/26`.