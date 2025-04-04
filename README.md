FASE 1 ANALISIS DE REQUIRIMIENTOS Y DISEÑO

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


FASE 2 DISEÑO TECNICO

clientes_conectados = []
lock_clientes = Lock()  # Protege la lista de clientes
 
def manejar_cliente(cliente):
    while cliente.esta_activo():
        mensaje = cliente.recibir()
        if mensaje:
            # Sección crítica: acceso a lista de clientes
            with lock_clientes:
                for otro_cliente in clientes_conectados:
                    if otro_cliente != cliente:
                        otro_cliente.enviar(mensaje)
 
def servidor_principal():
    socket_servidor = crear_socket()
    socket_servidor.escuchar()
 
    while True:
        nuevo_cliente = socket_servidor.aceptar()
        with lock_clientes:  # Sección crítica: agregar cliente
            clientes_conectados.append(nuevo_cliente)
 
        crear_hilo(manejar_cliente, nuevo_cliente)
