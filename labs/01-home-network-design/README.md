# Laboratorio 01: Diseño de una red doméstica segmentada

## Tema

Diseño de una red doméstica o de pequeña oficina segmentada.

## Objetivo

Diseñar una red local básica segmentada, separando los dispositivos de acuerdo con su función, nivel de confianza y necesidades de comunicación.

## Aprendizajes esperados

Al finalizar este laboratorio, el estudiante será capaz de:

- Identificar dispositivos comunes dentro de una red doméstica o de pequeña oficina.
- Agrupar dispositivos según su propósito.
- Asignar segmentos lógicos de red.
- Comprender por qué la segmentación mejora la organización y la seguridad.
- Representar un diseño de red mediante un diagrama simple.
- Justificar decisiones de diseño usando razonamiento técnico.

## Escenario

Una pequeña oficina en casa cuenta con los siguientes dispositivos:

| Tipo de dispositivo | Cantidad |
|---|---:|
| Computadoras personales | 3 |
| Teléfonos inteligentes | 2 |
| Smart TV | 1 |
| Dispositivos IoT | 4 |
| Impresora | 1 |
| Servidor web local | 1 |
| Dispositivos de invitados | Variable |

El propietario desea organizar la red para mejorar la seguridad y facilitar la administración.

La red debe separar los dispositivos personales, dispositivos de invitados, dispositivos IoT y servicios locales.

## Segmentos de red propuestos

| Segmento | Red | Propósito |
|---|---|---|
| Red principal | 192.168.10.0/24 | Computadoras personales, teléfonos y dispositivos confiables |
| Red de invitados | 192.168.20.0/24 | Acceso temporal para visitantes |
| Red IoT | 192.168.30.0/24 | Smart TV y dispositivos inteligentes |
| Red de servidores | 192.168.40.0/24 | Servidor web local y servicios internos |

## Asignación sugerida de dispositivos

| Dispositivo | Segmento sugerido | Razón |
|---|---|---|
| Computadora personal 1 | Red principal | Dispositivo confiable del usuario |
| Computadora personal 2 | Red principal | Dispositivo confiable del usuario |
| Computadora personal 3 | Red principal | Dispositivo confiable del usuario |
| Teléfono inteligente 1 | Red principal | Dispositivo confiable del usuario |
| Teléfono inteligente 2 | Red principal | Dispositivo confiable del usuario |
| Smart TV | Red IoT | Dispositivo conectado a internet con menor nivel de confianza |
| Dispositivo IoT 1 | Red IoT | Dispositivo inteligente separado de los equipos personales |
| Dispositivo IoT 2 | Red IoT | Dispositivo inteligente separado de los equipos personales |
| Dispositivo IoT 3 | Red IoT | Dispositivo inteligente separado de los equipos personales |
| Dispositivo IoT 4 | Red IoT | Dispositivo inteligente separado de los equipos personales |
| Impresora | Red principal o red de servidores | Dispositivo interno compartido |
| Servidor web local | Red de servidores | Servicio interno que debe estar separado |
| Dispositivos de invitados | Red de invitados | Dispositivos temporales y no confiables |

## Diagrama básico de red

```txt
                         Internet
                            |
                         Router
                            |
        ------------------------------------------------
        |                  |                  |         |
 Red principal      Red de invitados      Red IoT    Red de servidores
192.168.10.0/24     192.168.20.0/24   192.168.30.0/24 192.168.40.0/24
        |                  |                  |         |
 PCs, teléfonos       Invitados        Smart TV, IoT  Servidor web local
 Impresora
```

## Reglas básicas de comunicación

Se sugieren las siguientes reglas para la red segmentada:

| Origen | Destino | Acción | Razón |
|---|---|---|---|
| Red principal | Internet | Permitir | Los usuarios confiables necesitan acceso a internet |
| Red de invitados | Internet | Permitir | Los invitados necesitan acceso básico a internet |
| Red de invitados | Red principal | Bloquear | Los invitados no deben acceder a dispositivos personales |
| Red de invitados | Red de servidores | Bloquear | Los invitados no deben acceder a servicios internos |
| Red IoT | Internet | Permitir | Algunos dispositivos IoT requieren conexión con servicios en la nube |
| Red IoT | Red principal | Bloquear | Los dispositivos IoT no deben acceder a computadoras personales |
| Red principal | Red de servidores | Permitir | Los usuarios confiables pueden acceder a servicios internos |
| Red de servidores | Internet | Permitir de forma limitada | Los servidores pueden necesitar actualizaciones |
| Internet | Redes internas | Bloquear | El tráfico externo no debe entrar directamente a la red local |

## Actividades del estudiante

El estudiante deberá realizar las siguientes actividades:

1. Identificar todos los dispositivos del escenario.
2. Asignar cada dispositivo al segmento de red correspondiente.
3. Explicar por qué cada dispositivo pertenece a ese segmento.
4. Crear un diagrama de red usando diagrams.net, draw.io u otra herramienta.
5. Definir al menos cinco reglas de comunicación entre segmentos.
6. Explicar cómo la segmentación mejora la seguridad.
7. Responder las preguntas del archivo `questions.md`.

## Entregables esperados

El estudiante deberá entregar:

- Tabla completa de asignación de dispositivos.
- Diagrama de red.
- Explicación breve de la estrategia de segmentación.
- Reglas de comunicación o firewall entre segmentos.
- Respuestas a las preguntas de análisis.

## Criterios de evaluación

| Criterio | Excelente | Bueno | Necesita mejorar |
|---|---|---|---|
| Clasificación de dispositivos | Todos los dispositivos están correctamente asignados | La mayoría de los dispositivos están correctamente asignados | La asignación es confusa o incorrecta |
| Segmentación de red | Los segmentos son lógicos y están justificados | Los segmentos son mayormente correctos | La segmentación carece de razonamiento técnico |
| Calidad del diagrama | El diagrama es claro y organizado | El diagrama es comprensible | El diagrama está incompleto o es confuso |
| Razonamiento de seguridad | Las reglas están bien justificadas | Algunas reglas están justificadas | Faltan reglas o están mal explicadas |
| Documentación | El trabajo es claro y completo | El trabajo es mayormente claro | El trabajo está incompleto |

## Conclusión

La segmentación de red ayuda a organizar dispositivos, reducir comunicaciones innecesarias y mejorar la seguridad. Incluso en una red doméstica o de pequeña oficina, separar dispositivos confiables, invitados, IoT y servidores puede disminuir riesgos y facilitar la administración.