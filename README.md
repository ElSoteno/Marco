# Servidor de Chat Multihilo
 
## Objetivo

Desarrollar un servidor de chat concurrente que permita la interacción en tiempo real entre múltiples clientes conectados simultáneamente, usando programación multihilo en Python.
 
## Requerimientos Técnicos

- Python 3.x

- Librerías: `socket`, `threading`, `queue`, `time`

- Sistema operativo compatible: Linux, Windows, macOS
 
## User Stories

- Como cliente, quiero conectarme al servidor para empezar a chatear.

- Como cliente, quiero enviar mensajes al servidor para que otros los reciban.

- Como cliente, quiero recibir mensajes de otros clientes.

- Como servidor, quiero llevar un registro de clientes conectados.
 
## Requerimientos Priorizados
 
| Funcionalidad                                                  | Prioridad    |

|----------------------------------------------------------------|--------------|

| Conexión de múltiples clientes al servidor.                    | Must-Have    |

| Envío y recepción de mensajes entre clientes.                  | Must-Have    |

| Mantenimiento de lista de clientes con protección (`Lock`).    | Must-Have    |

| Cierre adecuado de sesión de cliente.                          | Nice-to-Have |

| Mejorar rendimiento con `ThreadPoolExecutor`.                  | Nice-to-Have |

 