# Diseño de redes locales

## Introducción

El diseño de una red local consiste en organizar los dispositivos, servicios y reglas de comunicación dentro de una infraestructura de red. Una red bien diseñada facilita la administración, mejora la seguridad y permite identificar problemas con mayor rapidez.

En una red doméstica, escolar o de pequeña oficina, es común encontrar diferentes tipos de dispositivos conectados al mismo router. Sin embargo, no todos los dispositivos tienen el mismo nivel de confianza ni las mismas necesidades de comunicación.

Por esa razón, una buena práctica consiste en separar la red en segmentos lógicos.

## ¿Qué es una red local?

Una red local, también conocida como LAN, es una red que conecta dispositivos dentro de un área limitada, como una casa, una oficina, un laboratorio o una escuela.

Algunos dispositivos comunes dentro de una red local son:

- Computadoras personales.
- Teléfonos inteligentes.
- Impresoras.
- Cámaras de seguridad.
- Televisiones inteligentes.
- Servidores locales.
- Dispositivos IoT.
- Puntos de acceso inalámbrico.
- Routers y switches.

## ¿Qué es la segmentación de red?

La segmentación de red consiste en dividir una red en partes más pequeñas para separar dispositivos según su función, nivel de confianza o necesidades de comunicación.

Por ejemplo, en lugar de tener todos los dispositivos dentro de una sola red, se pueden crear segmentos como:

| Segmento | Propósito |
|---|---|
| Red principal | Dispositivos personales y confiables |
| Red de invitados | Dispositivos temporales de visitantes |
| Red IoT | Dispositivos inteligentes o de menor confianza |
| Red de servidores | Servicios internos como páginas web, archivos o aplicaciones |

## ¿Por qué segmentar una red?

Segmentar una red ayuda a mejorar la seguridad y la administración.

Si todos los dispositivos están conectados a la misma red sin restricciones, cualquier equipo podría intentar comunicarse con los demás. Esto puede representar un riesgo si un dispositivo está infectado, mal configurado o pertenece a un usuario externo.

La segmentación permite controlar mejor la comunicación entre dispositivos.

## Beneficios de la segmentación

### 1. Mayor seguridad

Separar dispositivos reduce el riesgo de que un equipo comprometido afecte a toda la red.

Por ejemplo, si un dispositivo IoT es vulnerable, la segmentación puede evitar que acceda directamente a computadoras personales o servidores internos.

### 2. Mejor organización

Cada grupo de dispositivos tiene una función específica. Esto facilita saber dónde debe estar conectado cada equipo.

Por ejemplo:

- Computadoras y teléfonos personales en la red principal.
- Visitantes en la red de invitados.
- Cámaras, sensores y Smart TV en la red IoT.
- Servidores locales en la red de servidores.

### 3. Control de acceso

La segmentación permite definir reglas de comunicación.

Por ejemplo:

| Origen | Destino | Acción |
|---|---|---|
| Red principal | Servidor local | Permitir |
| Red de invitados | Red principal | Bloquear |
| Red IoT | Red principal | Bloquear |
| Internet | Redes internas | Bloquear |

### 4. Facilidad para diagnosticar problemas

Cuando la red está organizada por segmentos, es más fácil identificar dónde ocurre un problema.

Por ejemplo, si los dispositivos IoT no tienen internet, el administrador puede revisar únicamente la red IoT en lugar de analizar toda la infraestructura.

## Segmentos propuestos para el escenario base

Para este proyecto se utiliza el siguiente escenario base:

| Segmento | Red | Uso principal |
|---|---|---|
| Red principal | 192.168.10.0/24 | Computadoras personales, teléfonos y dispositivos confiables |
| Red de invitados | 192.168.20.0/24 | Dispositivos temporales de visitantes |
| Red IoT | 192.168.30.0/24 | Smart TV, cámaras, sensores y dispositivos inteligentes |
| Red de servidores | 192.168.40.0/24 | Servidor web local y servicios internos |

La notación `/24` indica que cada red puede tener hasta 254 direcciones IP utilizables para dispositivos.

Por ejemplo, la red `192.168.10.0/24` puede usar direcciones como:

```txt
192.168.10.1
192.168.10.2
192.168.10.3
...
192.168.10.254
```

Normalmente, la primera dirección utilizable se asigna al router o puerta de enlace.

Ejemplo:

| Segmento | Puerta de enlace sugerida |
|---|---|
| Red principal | 192.168.10.1 |
| Red de invitados | 192.168.20.1 |
| Red IoT | 192.168.30.1 |
| Red de servidores | 192.168.40.1 |

## Red principal

La red principal contiene los dispositivos confiables del usuario o de la organización.

Ejemplos:

- Computadoras personales.
- Laptops.
- Teléfonos del propietario.
- Tabletas de uso personal.
- Impresora interna, si solo será usada por usuarios confiables.

Esta red normalmente tiene más permisos que las demás, ya que desde aquí se puede acceder a servicios internos como servidores, impresoras o sistemas administrativos.

## Red de invitados

La red de invitados se utiliza para dispositivos temporales que no pertenecen directamente al propietario de la red.

Ejemplos:

- Teléfonos de visitantes.
- Laptops de invitados.
- Dispositivos conectados de forma temporal.

Esta red debe tener acceso a internet, pero no debería tener acceso a computadoras personales, servidores internos ni dispositivos administrativos.

Regla recomendada:

```txt
Permitir: Red de invitados -> Internet
Bloquear: Red de invitados -> Redes internas
```

## Red IoT

La red IoT contiene dispositivos inteligentes o conectados a internet.

Ejemplos:

- Smart TV.
- Cámaras inteligentes.
- Bocinas inteligentes.
- Sensores.
- Enchufes inteligentes.
- Asistentes de voz.
- Focos inteligentes.

Estos dispositivos pueden ser útiles, pero muchas veces tienen menor nivel de seguridad que una computadora personal. Algunos reciben pocas actualizaciones, usan contraseñas débiles o dependen de servicios externos.

Por eso se recomienda separarlos de la red principal.

Regla recomendada:

```txt
Permitir: Red IoT -> Internet
Bloquear: Red IoT -> Red principal
Bloquear: Red IoT -> Red de servidores, salvo excepciones justificadas
```

## Red de servidores

La red de servidores contiene servicios internos que pueden ser utilizados por los dispositivos confiables.

Ejemplos:

- Servidor web local.
- Servidor de archivos.
- Servidor DNS interno.
- Servidor de pruebas.
- Aplicaciones internas.

Esta red debe estar separada porque los servidores suelen concentrar información o servicios importantes.

Regla recomendada:

```txt
Permitir: Red principal -> Red de servidores
Bloquear: Red de invitados -> Red de servidores
Bloquear: Internet -> Red de servidores, salvo publicación controlada de servicios
```

## Importancia del firewall

El firewall permite definir qué tráfico puede pasar entre segmentos y qué tráfico debe bloquearse.

Sin reglas de firewall, segmentar la red pierde parte de su utilidad, ya que los dispositivos podrían seguir comunicándose sin restricciones.

Una política básica de firewall puede seguir esta lógica:

1. Bloquear todo el tráfico no autorizado.
2. Permitir solo las comunicaciones necesarias.
3. Separar invitados e IoT de los dispositivos personales.
4. Permitir que la red principal acceda a servicios internos.
5. Bloquear accesos directos desde internet hacia la red interna.

## Ejemplo de política básica

| Origen | Destino | Acción | Justificación |
|---|---|---|---|
| Red principal | Internet | Permitir | Los usuarios confiables requieren navegación |
| Red principal | Red de servidores | Permitir | Los usuarios confiables pueden usar servicios internos |
| Red de invitados | Internet | Permitir | Los invitados solo necesitan navegación básica |
| Red de invitados | Red principal | Bloquear | Protege dispositivos personales |
| Red de invitados | Red de servidores | Bloquear | Protege servicios internos |
| Red IoT | Internet | Permitir | Algunos dispositivos IoT requieren conexión externa |
| Red IoT | Red principal | Bloquear | Reduce riesgo hacia equipos personales |
| Internet | Redes internas | Bloquear | Evita accesos externos no autorizados |

## Errores comunes en el diseño de redes

Al diseñar una red, es común cometer errores como:

- Conectar todos los dispositivos a una sola red sin separación.
- Permitir que invitados accedan a dispositivos personales.
- Colocar cámaras, Smart TV o sensores en la misma red que las computadoras.
- No documentar direcciones IP, dispositivos o reglas.
- Usar contraseñas débiles en el router o red Wi-Fi.
- No actualizar el firmware de dispositivos de red.
- Permitir acceso desde internet sin reglas claras.

## Buenas prácticas

Algunas buenas prácticas para diseñar una red local son:

- Separar dispositivos por función.
- Usar nombres claros para cada segmento.
- Documentar las direcciones IP utilizadas.
- Limitar el acceso de invitados.
- Aislar dispositivos IoT.
- Proteger servicios internos.
- Usar contraseñas seguras.
- Mantener actualizado el router y los dispositivos principales.
- Revisar periódicamente las reglas de firewall.

## Relación con el Laboratorio 01

El Laboratorio 01 aplica los conceptos de este documento mediante el diseño de una red doméstica segmentada.

El estudiante debe analizar los dispositivos disponibles, asignarlos a segmentos adecuados, crear un diagrama de red y justificar las reglas básicas de comunicación.

Este laboratorio no busca configurar equipos reales todavía. Su objetivo principal es comprender la lógica del diseño de redes antes de avanzar hacia configuraciones más técnicas.

## Conclusión

El diseño de redes no consiste únicamente en conectar dispositivos a internet. Una red bien diseñada debe considerar seguridad, organización, administración y control de acceso.

La segmentación permite separar dispositivos confiables, invitados, dispositivos IoT y servidores internos. Esto reduce riesgos, facilita el mantenimiento y mejora la comprensión de la infraestructura de red.