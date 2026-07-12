# VLANs conceptuales

## Introducción

Una VLAN, o red de área local virtual, permite separar dispositivos dentro de una misma infraestructura física de red.

En una red tradicional simple, todos los dispositivos conectados al mismo switch o router suelen pertenecer a la misma red local. Esto significa que computadoras, celulares, cámaras, impresoras, Smart TV y dispositivos de invitados podrían estar dentro del mismo segmento.

Una VLAN permite separar esos dispositivos de forma lógica, aunque físicamente estén conectados al mismo switch o al mismo punto de acceso inalámbrico.

## ¿Qué significa VLAN?

VLAN significa:

```txt
Virtual Local Area Network
```

En español:

```txt
Red de área local virtual
```

La palabra importante es **virtual**, porque la separación no depende necesariamente de tener varios switches físicos.

En lugar de comprar un switch para cada red, se puede usar un switch administrable y crear varias redes lógicas dentro del mismo equipo.

## Problema sin VLANs

Supongamos que una pequeña oficina tiene un solo router y un solo switch.

Todos los dispositivos están conectados a la misma red:

```txt
192.168.10.0/24
```

En esa red están:

```txt
Computadoras personales
Celulares
Impresora
Smart TV
Cámaras
Dispositivos IoT
Invitados
Servidor web local
```

El problema es que todos comparten el mismo segmento de red.

Esto puede generar riesgos como:

- Invitados intentando acceder a computadoras personales.
- Dispositivos IoT comunicándose con servidores internos.
- Cámaras o Smart TV dentro de la misma red que equipos importantes.
- Dificultad para aplicar reglas de seguridad.
- Mayor desorden en la administración de la red.

## Solución con VLANs

Con VLANs, los dispositivos pueden separarse de forma lógica.

Ejemplo:

| VLAN | Nombre | Subred asociada | Uso |
|---:|---|---|---|
| 10 | Principal | 192.168.10.0/24 | Computadoras y teléfonos confiables |
| 20 | Invitados | 192.168.20.0/24 | Dispositivos temporales |
| 30 | IoT | 192.168.30.0/24 | Cámaras, Smart TV, sensores |
| 40 | Servidores | 192.168.40.0/24 | Servidor web local y servicios internos |

Cada VLAN representa un segmento lógico diferente.

## VLAN y subred no son exactamente lo mismo

Este punto es muy importante.

Una VLAN y una subred están relacionadas, pero no son lo mismo.

| Concepto | Función |
|---|---|
| VLAN | Separa dispositivos a nivel de capa 2 |
| Subred | Separa direcciones IP a nivel de capa 3 |

Dicho de forma simple:

```txt
La VLAN separa el tráfico dentro del switch.
La subred separa las direcciones IP.
```

Normalmente, cada VLAN tiene su propia subred.

Ejemplo:

| VLAN | Subred |
|---:|---|
| VLAN 10 | 192.168.10.0/24 |
| VLAN 20 | 192.168.20.0/24 |
| VLAN 30 | 192.168.30.0/24 |
| VLAN 40 | 192.168.40.0/24 |

Pero técnicamente no son el mismo concepto.

## Ejemplo visual

Sin VLANs:

```txt
Internet
   |
Router
   |
Switch
   |
------------------------------------------------
|        |        |        |        |          |
PC     Celular   Cámara   Invitado Servidor   TV

Todos en la misma red:
192.168.10.0/24
```

Con VLANs:

```txt
Internet
   |
Router / Firewall
   |
Switch administrable
   |
------------------------------------------------
|              |              |                |
VLAN 10        VLAN 20        VLAN 30          VLAN 40
Principal      Invitados      IoT              Servidores

192.168.10.0   192.168.20.0   192.168.30.0     192.168.40.0
```

Aunque todos los dispositivos estén conectados al mismo switch físico, quedan separados lógicamente.

## ¿Para qué sirven las VLANs?

Las VLANs sirven para:

- Separar dispositivos por función.
- Mejorar la seguridad.
- Organizar mejor la red.
- Reducir tráfico innecesario.
- Aplicar reglas de firewall entre segmentos.
- Separar invitados de dispositivos internos.
- Aislar dispositivos IoT.
- Administrar redes más grandes de forma ordenada.

## Relación entre VLANs, subredes y firewall

Para que una segmentación esté bien diseñada, normalmente se combinan tres elementos:

```txt
VLAN + Subred + Firewall
```

Cada uno cumple una función diferente.

| Elemento | Función |
|---|---|
| VLAN | Separa dispositivos dentro de la red local |
| Subred | Define el rango de direcciones IP |
| Firewall | Controla qué tráfico puede pasar entre segmentos |

Ejemplo:

```txt
VLAN 10 -> 192.168.10.0/24 -> Red principal
VLAN 20 -> 192.168.20.0/24 -> Red de invitados
VLAN 30 -> 192.168.30.0/24 -> Red IoT
VLAN 40 -> 192.168.40.0/24 -> Red de servidores
```

Después, el firewall define reglas como:

| Origen | Destino | Acción |
|---|---|---|
| VLAN 10 Principal | Internet | Permitir |
| VLAN 20 Invitados | Internet | Permitir |
| VLAN 20 Invitados | VLAN 10 Principal | Bloquear |
| VLAN 30 IoT | VLAN 10 Principal | Bloquear |
| VLAN 10 Principal | VLAN 40 Servidores | Permitir |
| Internet | VLANs internas | Bloquear |

## VLAN sin firewall

Una VLAN ayuda a separar tráfico, pero por sí sola no siempre define toda la política de seguridad.

Para controlar qué VLAN puede hablar con otra VLAN, se necesita un dispositivo que enrute y filtre tráfico, como:

- Router con soporte para VLANs.
- Firewall.
- Switch capa 3.
- pfSense.
- OPNsense.
- MikroTik.
- OpenWrt.
- UniFi.
- Omada.

Sin reglas de firewall, puede existir comunicación entre VLANs si el router la permite.

Por eso no basta con crear VLANs. También hay que controlar el tráfico entre ellas.

## ¿Qué es un puerto access?

Un puerto **access** pertenece a una sola VLAN.

Se usa normalmente para conectar dispositivos finales como:

- Computadora.
- Impresora.
- Cámara.
- Smart TV.
- Teléfono IP.
- Servidor.

Ejemplo:

```txt
Puerto 1 -> VLAN 10 -> Computadora
Puerto 2 -> VLAN 30 -> Cámara IoT
Puerto 3 -> VLAN 40 -> Servidor local
```

El dispositivo conectado al puerto access no necesita saber que existe una VLAN. El switch se encarga de colocar ese tráfico dentro de la VLAN correspondiente.

## Ejemplo de puertos access

| Puerto del switch | Dispositivo | VLAN |
|---:|---|---:|
| 1 | Computadora principal | 10 |
| 2 | Laptop | 10 |
| 3 | Impresora | 10 |
| 4 | Cámara inteligente | 30 |
| 5 | Smart TV | 30 |
| 6 | Servidor web local | 40 |

En este ejemplo, cada puerto pertenece a una VLAN específica.

## ¿Qué es un puerto trunk?

Un puerto **trunk** puede transportar tráfico de varias VLANs al mismo tiempo.

Se usa normalmente para conectar:

- Un switch con otro switch.
- Un switch con un router.
- Un switch con un firewall.
- Un switch con un punto de acceso inalámbrico que maneja varias redes Wi-Fi.

Ejemplo:

```txt
Switch administrable
   |
Puerto trunk
   |
Router / Firewall
```

Ese puerto puede transportar tráfico de varias VLANs:

```txt
VLAN 10
VLAN 20
VLAN 30
VLAN 40
```

## Diferencia entre access y trunk

| Tipo de puerto | Uso | VLANs que transporta |
|---|---|---|
| Access | Dispositivo final | Una sola VLAN |
| Trunk | Conexión entre equipos de red | Varias VLANs |

Ejemplo simple:

```txt
Puerto access:
PC -> VLAN 10

Puerto trunk:
Switch -> Router -> VLAN 10, 20, 30, 40
```

## VLANs y redes Wi-Fi

Las VLANs también pueden usarse con redes Wi-Fi.

Un punto de acceso avanzado puede tener varios SSID.

Un SSID es el nombre de una red Wi-Fi.

Ejemplo:

| SSID | VLAN | Subred |
|---|---:|---|
| Casa-Principal | 10 | 192.168.10.0/24 |
| Casa-Invitados | 20 | 192.168.20.0/24 |
| Casa-IoT | 30 | 192.168.30.0/24 |

Esto permite que los dispositivos inalámbricos también estén separados.

Ejemplo:

```txt
Wi-Fi Casa-Principal -> VLAN 10
Wi-Fi Casa-Invitados -> VLAN 20
Wi-Fi Casa-IoT       -> VLAN 30
```

## Ejemplo realista de red doméstica avanzada

```txt
Internet
   |
Proveedor de internet
   |
Módem / ONT
   |
Router / Firewall con soporte VLAN
   |
Puerto trunk
   |
Switch administrable
   |
------------------------------------------------
|              |              |                |
PCs            Invitados      IoT              Servidor
VLAN 10        VLAN 20        VLAN 30          VLAN 40
```

Y para Wi-Fi:

```txt
Punto de acceso con múltiples SSID
   |
SSID Principal -> VLAN 10
SSID Invitados -> VLAN 20
SSID IoT       -> VLAN 30
```

## Limitaciones de routers de proveedor

Muchos routers entregados por proveedores de internet no permiten configurar VLANs internas avanzadas.

Normalmente ofrecen funciones básicas como:

- Red Wi-Fi principal.
- Red Wi-Fi de invitados.
- DHCP básico.
- Reenvío de puertos.
- Configuración limitada de firewall.

Pero no siempre permiten:

- Crear varias VLANs.
- Asignar VLANs a puertos físicos.
- Crear reglas avanzadas entre VLANs.
- Usar múltiples SSID con VLANs.
- Definir políticas de seguridad detalladas.

Por eso, para una red segmentada más completa, muchas veces se requiere equipo adicional.

## Equipo que puede usarse para VLANs

Para implementar VLANs reales se puede usar:

- Router compatible con VLANs.
- Firewall dedicado.
- Switch administrable.
- Punto de acceso con soporte para múltiples SSID y VLANs.
- Software como pfSense u OPNsense.
- Equipos MikroTik, UniFi, Omada, OpenWrt, entre otros.

En este proyecto, la versión 1.0 trabaja VLANs de forma conceptual. La configuración práctica puede agregarse en una versión posterior.

## Ejemplo de diseño para este proyecto

El diseño conceptual recomendado para el escenario base es:

| Segmento | VLAN | Subred | Dispositivos |
|---|---:|---|---|
| Red principal | 10 | 192.168.10.0/24 | Computadoras, laptops, teléfonos confiables |
| Red de invitados | 20 | 192.168.20.0/24 | Celulares y laptops de visitantes |
| Red IoT | 30 | 192.168.30.0/24 | Smart TV, cámaras, sensores |
| Red de servidores | 40 | 192.168.40.0/24 | Servidor web local |

## Reglas sugeridas entre VLANs

| Origen | Destino | Acción | Justificación |
|---|---|---|---|
| VLAN 10 Principal | Internet | Permitir | Usuarios confiables necesitan navegación |
| VLAN 20 Invitados | Internet | Permitir | Invitados solo requieren acceso básico |
| VLAN 20 Invitados | VLAN 10 Principal | Bloquear | Protege dispositivos personales |
| VLAN 20 Invitados | VLAN 40 Servidores | Bloquear | Evita acceso a servicios internos |
| VLAN 30 IoT | Internet | Permitir | Algunos dispositivos IoT requieren servicios externos |
| VLAN 30 IoT | VLAN 10 Principal | Bloquear | Reduce riesgo hacia computadoras personales |
| VLAN 10 Principal | VLAN 40 Servidores | Permitir | Usuarios confiables pueden acceder al servidor |
| Internet | VLANs internas | Bloquear | Evita accesos externos no autorizados |

## Error común: pensar que VLAN y Wi-Fi de invitados son lo mismo

Una red Wi-Fi de invitados puede usar una VLAN internamente, pero no siempre es así.

En routers domésticos básicos, la red de invitados puede estar aislada mediante una función simple del router, sin que el usuario vea o configure VLANs directamente.

En redes más avanzadas, una red de invitados normalmente se configura así:

```txt
SSID Invitados -> VLAN 20 -> Subred 192.168.20.0/24 -> Reglas de firewall
```

## Error común: crear subredes sin VLANs

También es común pensar que con solo crear varias subredes ya existe separación completa.

Pero si todos los dispositivos están conectados al mismo segmento físico sin VLANs, la separación puede quedar incompleta o depender totalmente del router.

En una red bien diseñada, se busca alinear:

```txt
Segmento lógico = VLAN + Subred + reglas de firewall
```

Ejemplo:

```txt
Red IoT = VLAN 30 + 192.168.30.0/24 + reglas de bloqueo hacia red principal
```

## Error común: permitir comunicación total entre VLANs

Crear VLANs y luego permitir que todas se comuniquen libremente entre sí reduce mucho el beneficio de la segmentación.

Si la VLAN de invitados puede acceder a la VLAN principal, entonces la separación pierde sentido.

La idea es permitir solo el tráfico necesario.

## Buenas prácticas

Al trabajar con VLANs, se recomienda:

- Usar nombres claros para cada VLAN.
- Documentar el número de VLAN.
- Asociar una subred por VLAN.
- Definir reglas de firewall entre VLANs.
- Separar invitados de dispositivos confiables.
- Aislar dispositivos IoT.
- No permitir tráfico innecesario entre segmentos.
- Reservar una VLAN para administración si la red crece.
- Documentar puertos access y trunk.
- Probar conectividad después de cada cambio.

## Tabla de documentación sugerida

| VLAN | Nombre | Subred | Gateway | DHCP | Uso |
|---:|---|---|---|---|---|
| 10 | Principal | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.100-199 | Usuarios confiables |
| 20 | Invitados | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.100-199 | Visitantes |
| 30 | IoT | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.100-199 | Dispositivos inteligentes |
| 40 | Servidores | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.100-199 | Servicios internos |

## Preguntas de repaso

1. ¿Qué es una VLAN?
2. ¿Qué problema resuelve una VLAN?
3. ¿Cuál es la diferencia entre una VLAN y una subred?
4. ¿Por qué normalmente cada VLAN tiene su propia subred?
5. ¿Qué es un puerto access?
6. ¿Qué es un puerto trunk?
7. ¿Para qué sirve asociar un SSID a una VLAN?
8. ¿Por qué no conviene que la VLAN de invitados acceda a la VLAN principal?
9. ¿Qué papel cumple el firewall entre VLANs?
10. ¿Por qué muchos routers de proveedor no son suficientes para una segmentación avanzada?

## Relación con los laboratorios anteriores

El Laboratorio 01 trabaja el diseño general de una red segmentada.

El Laboratorio 02 trabaja el cálculo de subredes y rangos IP.

Este documento agrega el concepto de VLAN para explicar cómo esa segmentación puede implementarse de forma lógica dentro de una red física.

La relación queda así:

```txt
Laboratorio 01 -> Diseño de segmentos
Laboratorio 02 -> Cálculo de subredes
VLANs conceptuales -> Separación lógica dentro de la infraestructura
```

## Conclusión

Las VLANs permiten separar dispositivos de forma lógica dentro de una misma infraestructura física. Son fundamentales para organizar redes, aislar dispositivos de menor confianza y aplicar reglas de seguridad entre segmentos.

Una VLAN no reemplaza a una subred ni a un firewall. En una red bien diseñada, las VLANs trabajan junto con subredes y reglas de firewall.

Para este proyecto, las VLANs se estudian primero de forma conceptual. En una versión posterior se pueden implementar mediante simuladores, switches administrables o firewalls reales.