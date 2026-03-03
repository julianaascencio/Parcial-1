# Parcial corte I
## Integrantes
Lesly Juliana Ascencio Peréz

# Punto 1
## Escenario
Eres un analista de red y debes investigar el comportamiento de la red de una oficina pequeña. Para ello, realizas una captura de tráfico en el equipo de un usuario mientras este realiza tareas cotidianas: navegar por internet (HTTP/HTTPS), revisar su correo y compartir archivos. Adicionalmente, usas la CMD para diagnosticar la conectividad.

## a) Explicar la diferencia fundamental entre la latencia y el jitter. ¿Cuál de estas dos métricas tendría un impacto más negativo en una llamada VoIP y por qué?

### Diferencia entre latencia y jitter
### Latencia
Es el tiempo que tarda un paquete de datos en ir desde el origen hasta el destino. Se mide en milisegundos (ms).
### Jitter:
Es la variación en el tiempo de llegada de los paquetes.

### ¿Cuál afecta más una llamada VoIP y por qué?
El jitter afecta más negativamente a una llamada VoIP. Porque en una llamada de voz los paquetes deben llegar en orden y con tiempos constantes.

Si hay mucho jitter: 
- La voz se escucha entrecortada.
- Se pierden partes de la conversación.
- Hay distorsión o retrasos irregulares.
  
Aunque la latencia alta también afecta (porque genera retraso en la conversación), el jitter provoca una experiencia más inestable y molesta.

## b) Una aplicación envía datos usando protocolo TCP, mientras que otra usa UDP para la misma tarea de transmisión de video. ¿Cuál es más eficiente en términos de throughput y cuál ofrece mayor control de la pérdida de paquetes? Justifique su respuesta basándote en la "anatomía" de sus cabeceras.

UDP es más eficiente en throughput porque no depende de confirmaciones (ACK), no retransmite paquetes y tiene menor sobrecarga en su cabecera. Por esta razón se usa en streaming y videollamadas, donde es más importante la velocidad que la entrega perfecta de los datos. En cambio, TCP ofrece mayor control de pérdida de paquetes porque incluye número de secuencia, confirmaciones, control de flujo y de congestión; si un paquete se pierde lo retransmite, mientras que UDP no verifica ni reenvía los datos perdidos.

## c) Al ejecutar el comando “arp-a” en la CMD de Windows, se obtienen una lista de direcciones IP y direcciones físicas. ¿Qué protocolo de la suite TCP/IP llena esta tabla y cuál es su función principal dentro de una red local? Relacionar la respuesta con la estructura de una trama Ethernet.

Al ejecutar el comando arp -a se muestra una tabla que es llenada por el protocolo ARP, cuya función es relacionar una dirección IP con una dirección física (MAC) dentro de una red local. Básicamente, cuando un equipo quiere enviar datos a otra IP en la misma red, utiliza ARP para preguntar cuál es su dirección MAC y así poder establecer la comunicación.

![arp -a](https://github.com/user-attachments/assets/26429c36-0a75-4bae-987c-2372410e1f77)

## d) Mencionar dos diferencias clave entre las arquitecturas SNMPv2c y SNMPv3. Enfocarse en los aspectos de seguridad y el tipo de mensajes que manejan.

Dos diferencias claves entre SNMPv2c y SNMPv3 son la seguridad y el manejo de los mensajes, es decir, SNMPv2c hace uso de un sistema de seguridad muy basico donde hace uso de contraseñas sin cifrado, por lo que lo hace menos seguro, mientras que SNMPv3 hace uso de la autentificación, cifrado y control de acceso.
En cuanto a los mensajes, aunque ambos como Get y Set, SNMPv3 tiene una mayor protección de los mensajes transmitidos para evitar intercepciones o modificaciones.

## e) Define qué es un OID y cuál es su relación con la MIB. Si un administrador quiere saber la cantidad de bytes que ha recibido una interfaz de red, ¿qué operación SNMP (Get, Set, Trap) debe utilizar y por qué no sería adecuado usar un Trap para esto?

Un OID es como el identificador único de una variable dentro de la MIB. La MIB es básicamente una base de datos donde están organizados todos los datos que se pueden consultar en un dispositivo de red.
Si el administrador quiere saber cuántos bytes ha recibido una interfaz, debe usar la operación Get, porque solo necesita consultar la información. No sería correcto usar un Trap, ya que el Trap es una notificación automática que se envía cuando ocurre un evento, no sirve para pedir datos específicos en ese momento.


# Punto 2
## Escenario
Imagine que abres el archivo de captura y filtra por “http”. Encuentras el siguiente paquete con estos datos (versión simplificada de una trama Ethernet con un segmento TCP):

<img width="321" height="64" alt="image" src="https://github.com/user-attachments/assets/acd6c5cd-0bbf-4c7c-bcab-969b393d876a" />

## a) Identificar y explicar cada uno de los campos de la cabecera Ethernet. ¿Qué significa el valor 0x0800 en el campo "Tipo"?


