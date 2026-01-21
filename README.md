# Chat_Rober - Chat Grupal en Java con Sockets y JavaFX

## Descripción

**Chat_Rober** es una aplicación de chat grupal desarrollada en **Java**, utilizando **sockets TCP** para la comunicación y **JavaFX** para la interfaz gráfica.  

Permite que múltiples usuarios se conecten al mismo tiempo, envíen y reciban mensajes en tiempo real, y vean el historial completo de la sesión.  

---

## Objetivos del Proyecto

- Crear un **chat grupal** donde todos los usuarios puedan comunicarse simultáneamente.  
- Implementar un **servidor multihilo** capaz de manejar varios clientes al mismo tiempo.  
- Mostrar un **historial de mensajes** a los nuevos usuarios que se conecten.  
- Desarrollar una **interfaz intuitiva** con JavaFX para enviar y recibir mensajes.  

---

## Flujo de la Aplicación

### 1. Servidor
- Se ejecuta `EchoServerMultihilo`.
- Escucha en el puerto `8080` conexiones entrantes.
- Gestiona clientes mediante un **pool de hilos** para soporte multicliente.
- Cada cliente recibe un **identificador único** y el historial de mensajes acumulados.

### 2. Cliente
- Se ejecuta `HelloApplication`, que abre la ventana de chat.
- `EchoClient` establece la conexión con el servidor mediante TCP.
- Al conectarse, se solicita un **nombre de usuario**.
- El cliente recibe un **mensaje de bienvenida** y todo el historial previo de la sesión.

### 3. Comunicación
- Los mensajes se escriben en un `TextField` y se envían al servidor.
- El servidor guarda el mensaje y lo reenvía a todos los clientes conectados.
- Todos los clientes muestran los mensajes **en tiempo real** en un `TextArea`.

### 4. Gestión de Clientes
- Cada cliente es manejado por `ManejadorClienteMultihilo`.
- Enviar `"salir"` desconecta al cliente y notifica al resto.
- El servidor mantiene la **lista de clientes activos** para asegurar la comunicación grupal.

---

## Características Clave

- **Servidor Multihilo:** Hasta 10 clientes simultáneos (configurable), con `CopyOnWriteArrayList` y `AtomicInteger` para manejar concurrencia.  
- **Cliente Independiente:** Cada ventana representa un usuario, permitiendo simular múltiples usuarios en el mismo equipo.  
- **Interfaz Gráfica con JavaFX:**  
  - `TextArea` para mensajes (solo lectura).  
  - `TextField` para escribir mensajes.  
  - Botones para enviar mensajes y abrir nuevas ventanas de chat.  
- **Ingreso de Nombre de Usuario:** Cada cliente elige su nombre al conectarse.  
- **Historial de Sesión:** Los mensajes previos se muestran automáticamente a cada nuevo cliente.

---

## Estructura del Proyecto
com.example.chat_rober/
│
├── HelloApplication.java              # Clase principal que lanza la interfaz
├── HelloController.java               # Controlador de JavaFX
├── EchoClient.java                    # Cliente TCP para enviar y recibir mensajes
├── EchoServerMultihilo.java           # Servidor multihilo que gestiona los clientes
├── ManejadorClienteMultihilo.java     # Hilo que maneja la comunicación de un cliente
└── hello-view.fxml                    # Interfaz de usuario (JavaFX)

## Cómo Ejecutar

### Servidor
1. Ejecutar `EchoServerMultihilo.java`.
2. El servidor quedará escuchando en el puerto `8080`.

### Cliente
1. Ejecutar `HelloApplication.java`.
2. Ingresar un **nombre de usuario** en el diálogo que aparece.
3. Se abrirá la ventana de chat.
4. Puedes abrir varias ventanas para simular varios usuarios.

### Mensajes
- Escribir en el `TextField` y pulsar **Enviar**.  
- Los mensajes se muestran automáticamente en todos los clientes conectados.
