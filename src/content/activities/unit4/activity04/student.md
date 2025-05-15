#### Actividad 4: 

- ¿Qué es webRTC?
  
  Es una tecnologia de codigo abierto que permite la comuncacion en tiempo real entre navegadores sin usar plugins extras, proporciona APIS para la captura y transmisión de audio, videp y datos, facilitando la transmision de medios con peer-to-peer.
- ¿Cómo funciona webRTC?
  
  Bueno, esto lo que hace es qie establece conexiones directas entre los navegadores de ambos clientes, tipo como una negociacion en la que los clientes capturan los datos o medios, se establecen los Peer connections que transmiten directamente todo, se intercambia la info de conexion a traves del signaling server y con esos ICE, STUNT y TURN segun lo que entiendo se determina la mejor ruta de coexion para superar las restricciones.
  
- ¿Qué es un peer connection?
  
  He usado mucho este termino y llego mi momento de explicarlo, basicamente esta es la conexion directa entre dos navegadores que permite el intercambio de medios y datos en tiempo real. Esto quiere decir que despues de intercambiar informacion de señalizacion, se establece la conexion y se encarga de gestionar la trnasmision segura y eficiente de la info.
  
- ¿Qué es un data channel?
  
  Este es un canal de comunicacion adicional que se abre sobre la Peer connection, pertimiendo el envío de datos como texto o JSON, de forma bidireccional y en tiempo real
  
- ¿Qué es un media stream?

  Es un flujo de medios compuesto por una o varios audios o videos, estos streams son los que capturamos por medio de la camara y el mic y ya ahi se los transmitimos a otros users.
- ¿Qué es un ICE server?

  ICE significa Interactive Connectivity Establishment, este server es un componente del proceso de conexion del WebRTC, ayuda a los navegadores a descubirir y elegir la mejor ruta para comunicar los clientes, recopila la info sobre las direcciones de red y posibles candidatos de conexion.
- ¿Qué es un STUN server?

  STUNT es Session Traversal Utilities for NAT, este server permite a un cliente obtener su IP publica y direccion de puerto, falicitando la creacion de conexiones peer-to-peer a traves de direcciones de red.
- ¿Qué es un TURN server?

  TURN es Traversal Using Relays around NAT, el sercer actua como interruptor de datos entre clientes cuando una conexion directa no es posible por los firewalls, se usa como uuuultima opcion para garantizar que haya comunicación.
- ¿Qué es un signaling server?

  El signaling server es el componente encargado de intercambiar la info inicial necesaria para establecer la peer connection, no transmite los medios ni datos, solo facilita el proceso de negociacion.
