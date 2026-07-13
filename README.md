# Networking Teaching Labs

Repositorio académico con prácticas reproducibles para la enseñanza de fundamentos de redes de computadoras.

Este proyecto organiza laboratorios, diagramas, cuestionarios y rúbricas de evaluación para apoyar el aprendizaje de temas esenciales como diseño de redes, subredes, VLANs conceptuales, DNS, DHCP, análisis de tráfico con Wireshark, reglas básicas de firewall y despliegue de servicios locales.

## Versión actual

**Versión 1.0 — Fundamentos de redes para enseñanza**

Esta primera versión se enfoca en prácticas introductorias documentadas en Markdown. El objetivo principal es crear material didáctico claro, ordenado y reutilizable para estudiantes que inician en redes de computadoras, administración de sistemas o ciberseguridad básica.

## Objetivo general

Diseñar un conjunto de laboratorios didácticos de redes que permitan a los estudiantes comprender, practicar y evaluar conceptos esenciales de infraestructura de red mediante escenarios simples, documentados y reproducibles.

## Objetivos específicos

* Diseñar una red doméstica o de pequeña oficina segmentada por tipos de dispositivos.
* Explicar el uso de subredes para organizar equipos dentro de una red local.
* Describir el concepto de VLAN y su utilidad en la segmentación lógica.
* Documentar el funcionamiento básico de DNS y DHCP.
* Analizar tráfico de red mediante Wireshark.
* Aplicar reglas básicas de firewall para controlar la comunicación entre segmentos.
* Implementar un servidor web local como servicio de prueba dentro de una red.
* Crear cuestionarios y rúbricas para evaluar el aprendizaje de los estudiantes.

## Contenido del repositorio

```txt
networking-teaching-labs/
│
├── docs/
│   ├── network-design.md
│   ├── subnetting-guide.md
│   ├── vlan-concepts.md
│   ├── dns-dhcp.md
│   ├── firewall-basics.md
│   └── wireshark-analysis.md
│
├── labs/
│   ├── 01-home-network-design/
│   ├── 02-subnetting/
│   ├── 03-dns-dhcp/
│   ├── 04-wireshark-traffic-analysis/
│   ├── 05-basic-firewall-rules/
│   └── 06-local-web-server/
│
├── diagrams/
│
├── evaluation/
│   ├── rubrics.md
│   └── questionnaires.md
│
├── README.md
├── LICENSE
└── .gitignore
```

## Laboratorios incluidos

| Laboratorio | Tema                               | Descripción                                                                                        |
| ----------- | ---------------------------------- | -------------------------------------------------------------------------------------------------- |
| 01          | Diseño de red doméstica segmentada | El estudiante diseña una red local separando dispositivos personales, invitados, IoT y servidores. |
| 02          | Subredes                           | El estudiante calcula y asigna subredes para diferentes segmentos de red.                          |
| 03          | DNS y DHCP                         | El estudiante comprende la asignación automática de direcciones IP y la resolución de nombres.     |
| 04          | Análisis de tráfico con Wireshark  | El estudiante captura e interpreta tráfico básico de red.                                          |
| 05          | Reglas básicas de firewall         | El estudiante analiza reglas simples para permitir o bloquear tráfico.                             |
| 06          | Servidor web local                 | El estudiante despliega un servidor web básico dentro de una red local.                            |

## Escenario base

El escenario principal representa una red doméstica o de pequeña oficina que requiere separar sus dispositivos por seguridad, administración y organización.

Segmentos propuestos:

```txt
Red principal:       192.168.10.0/24
Red de invitados:    192.168.20.0/24
Red IoT:             192.168.30.0/24
Red de servidores:   192.168.40.0/24
```

Cada segmento representa un grupo de dispositivos con necesidades diferentes de comunicación y seguridad.

## Público objetivo

Este material está dirigido a estudiantes de nivel medio superior, técnico superior universitario o licenciatura que estén iniciando en redes de computadoras, administración de sistemas o fundamentos de ciberseguridad.

## Competencias desarrolladas

Al completar las prácticas, el estudiante será capaz de:

* Interpretar diagramas básicos de red.
* Identificar dispositivos dentro de una red local.
* Asignar direcciones IP de forma organizada.
* Comprender la función de DNS y DHCP.
* Explicar el propósito de segmentar una red.
* Analizar tráfico básico con Wireshark.
* Aplicar reglas básicas de firewall.
* Documentar una práctica técnica de forma clara.

## Herramientas sugeridas

* Wireshark
* diagrams.net / draw.io
* Navegador web
* Terminal o consola del sistema operativo
* Servidor web local con Python, Apache, Nginx o Docker
* Cisco Packet Tracer o GNS3 como herramientas opcionales para futuras versiones

## Estado del proyecto

Proyecto en desarrollo.

La versión 1.0 se enfoca en documentación, prácticas introductorias, diagramas conceptuales, cuestionarios y rúbricas de evaluación.

## Autor

Josué Isaí Sánchez Santos
Ingeniería en Sistemas Computacionales


## Licencias

El código, los scripts y las configuraciones se distribuyen bajo la licencia MIT.
El material educativo se distribuye bajo Creative Commons Atribución 4.0 Internacional (CC BY 4.0).
Consulta [LICENSING.md](LICENSING.md), [LICENSE](LICENSE) y [LICENSE-CONTENT](LICENSE-CONTENT).
