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

## c) Mencionar dos diferencias clave entre las arquitecturas SNMPv2c y SNMPv3. Enfocarse en los aspectos de seguridad y el tipo de mensajes que manejan.
Dos diferencias claves entre SNMPv2c y SNMPv3 son la seguridad y el manejo de los mensajes, es decir, SNMPv2c hace uso de un sistema de seguridad muy basico donde hace uso de contraseñas sin cifrado
