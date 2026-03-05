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

En la cabecera Ethernet aparecen varios campos importantes. Primero está la dirección MAC de destino, que en este caso es aa:bb:cc:dd:ee:ff, y sirve para indicar a qué dispositivo va dirigida la trama dentro de la red local. Luego está la dirección MAC de origen, que es 00:11:22:33:44:55, y muestra quién envía la información.
Después está el campo Tipo, que en este caso es 0x0800. Este valor significa que el protocolo encapsulado dentro de la trama es IPv4. Es decir, le indica al equipo que los datos que vienen después deben interpretarse como un paquete IPv4.

## b) En la cabecera IPv4, ¿qué significan los campos Protocolo y TTL? ¿Por qué es importante el TTL en red?

### Protocolo
Este campo indica que el protocolo de la capa de transporte está contenido dentro del paquete IP, es decir, le dice al sistema operativo a qué protocolo debe entregar los datos cuando el paquete llega sin destino.
### TTL
Este campo indica la cantidad maxima de saltos (routers) que un paquete puede atravesar en la red antes de ser descartado, es decir, cada vez que el paquete pasa por un router, el valor del TTL se redice en 1, cuando el paquete llega a 0, el paquete se elimina y normalmente el router envia un mensaje ICMP Time Esceeded al origen.

### Importancia del TTL en la red
El TTL es importante porque evita que los paquetes circulen indefinidamente en la red en caso de que exista un bucle de enrutamiento, si no existiera este campo, un paquete podría quedarse viajando eternamente entre routers, generando congestión y consumo innecesario de ancho de banda.

## c)En la cabecera TCP, explicar la función de los flags ACK y PSH. ¿Qué indica el “Puerto Destino: 80” sobre el servicio que intenta acceder?

### 1. Flag ACK (Acknowledgment)
Este Flag o bandera indica que el paquete está confirmando la recepción de datos anteriores enviados por otros dispositivos. Caundo este está activo, significa que el campo Acknowledgment Number es válido y que el receptor está infromando que recibió correctamente los datos hasta cierto número de secuencia.

### 2. Flag PSH (Push)
Este indica que los datos del segmento deben enviarse inmediatamente a la aplicación, sin esperar que el buffer se llene. Esto se usa cuando los datos deben ser procesados rápidamente por la aplicación en el destino.

### "Puerto Destino: 80"
el puerto destino 80 indica el servicio al que se está intentando acceder en el servidor. Este puerto esta asociado al protocolo HTTP, que s eusa para la comunicación entre navegadores y servidor web.

## d)Si este mismo paquete se enviara usando IPv6, ¿qué cabecera de IPv6 reemplazaría a la cabecera IPv4 mostrada y cúal seria ina mejora notable en su procesamiento por parte d elos routers?

Si el paquete se enviara usando IPv6, la cabecera IPv4 seria reemplazada por la cabecera de IPv6
Una mejora importante de IPv6 es que su cabecera es más simple y de tamaño fijo de 40 bytes, mientras que la de IPv4 puede variar de tamaño debido a los campos opcionales.

Gracias a la simplidad de la estructura, los routers pueden procesar los paquetes más rápido, se reduce la carga de procesamiento en los dispositivos de red y las opciones adicionales se manejan mediante extensiones, lo que evita que todos los routers tengan que analizarlas.


# Punto 3
## Diagnostico y gestión con herramientas de windows

## a) Ejecutar el siguiente comando y explicar:
### 1. ¿Qué información proporciona este comando que dariá un "ping" o un "tracert"?
### 2. Describir el proceso que sigue "pathping" para obtener sus resultados.

```bash
pathping 8.8.8.8
```

Al ejecutar el comando en mi CMD arroja la siguiente información

<img width="464" height="296" alt="image" src="https://github.com/user-attachments/assets/3bff2e7a-78e1-4911-aedf-38393000faf4" />

Se obtiene información sobre la ruta que siguen lso paquetes desde el equipo local hasta el servidor de Google y permite analizar la calidad de la conexion.
En el resultado obtenido se observan los siguientes saltos

### Salto 0- Equipo de Juli [172.22.51.220]
Corresponde al equipo local desde donde se ejecuta el comando. Esta dirección IP asignada al computador dentro de la red.

### Salto 1-172.22.51.1
Este es el getway o router de la red local; Se observa un RTT de 5ms, lo que indica un tiempo de respuesta muy bajo, normal dentro de una red local. Además, se muestra 0% de perdida de paquetes (0/100), lo que indica que la comunicación con el router funciona correctamente.

### Salto 2 -10.0.0.1
Este sería el siguiente router en la red, posiblemente parte de la red interna del proveedor o sistema de salida a internet

En el resultado aparece:
- RTT ---
- 100/100 = 100% de pérdida desde el origen
Esto significa que ese dispositivo no responde a las solicitudes ICMP, algo bastante común porque muchos routers bloquean este tipo de mensjaes por seguridad.
No necesariamente significa que la red este fallando.

### 1. ¿Qué información proporciona este comando que dariá un "ping" o un "tracert"?
El comando combina funciones de ping y de tracert, por lo que proporciona más infirmacion para el diagnostico de red.
Por un lado, como tracert, muestra la ruta que siguen los paquetes desde el equipo origen hasta el destino, indicando cada uno de los saltos por los que pasa la comunicación.
Por otro lado, como ping, permite medir el tiempo de respuesta (RTT) entre los dispositivos.

### 2. Describir el proceso que sigue pathping para obtener sus resultados
El comango pathping obtiene sus resultados en dos etapas principales.

### Primera etapa: descubrimiento de la ruta
Primero, el comando funciona de forma similar al comando tracert. Envía paquetes ICMP con valores TTL incrementales para identificar cada uno de los routers o saltos entre el equipo origen y el destini. Es de esta forma como se construye la lista completa de nodos por los que pasan los paquetes.

### Segunda etapa: análisis de calidad del enlace
Después de identificar la ruta, pathping envía múltiples paquetes a cada uno de los routers detectados durante aproximadamente 50 segundos. Con estos paquetes se calcula estadísticas como:

- Tiempo de respuesta
- Número de paquetes enviados y perdidos
- Porcentaje de pérdida de paquetes en cada nodo o enlace
Con esta información se puede determinar en qué punto de la red se esta producioendo pérdida de paquetes o problemas de conexión.

A continuación se muestra la ejecución del comando con resultados positivos 

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/56026409-aba8-4f7a-bc16-b9eb3ce5df55" />

## b) Escenario - Para monitorear un rputer de la oficina, decides usar SNMP. El router soporta SNMPv2c con la comunidad "public" de solo lectura.

### ¿Qué comando de windows (o herramienta de linea de comandos) podria utilizar para "caminar" por el árbol MIB y obtener todos los valores de la interfaz del router en la IP 192.168.1.1?
Para recorrer el árbol MIB y obtener los valores de la interfaz del router se puede utilizar la herramienta snmpwalk, aunque este no viene instalado en la linea de comandos de windows, se puede instalar y hacer uso del siguiente comando.

```bash
snpmwalk -v2c -c public 192.168.1.1
```

Donde:
- -v2c: indica que se usa la versión SNMPv2c
-  -c public: comunicad SNMP configurada en el router con permiso de lectura
-  192.168.1.1: dirección IP del router

Este comando permite recorrer el árbol MIB y mostrar todos los objetos disponibles, como información de interfaces, trafico, estado de puertos y estadísticas del router.

### Si el router envia un mensjae "authenticationFailure" trap al gestor SNP, ¿Qué evento lo ha provocado y cúal es la ventaja de recibir un Trap en lugar de estar consultando constantemente (polling) el estado del router?
La ventaja de los SNMP traps es que el dispositivo envía automaticamente una notificación cuando ocurre un evento, sin necesidad de que el gesto SNMP esté consultando constantemente.

Las principales ventajas son:
- Menor tráfico de red, porque no se realizan consultas periódicas.
- Respuesta más rapida ante eventos, ya que la alerta se envia inmediatamente
- Menos carga en el router y en el servidor de monitoreo.

En cambio, el polling requiere consultar repetidamente al dispositivo para concer su estado, lo que logra generar más consumo de recurso en la red.

# Punto 4
## Escenario
### Los estudiantes de compensar son desarrolladores que trabajan en un proyecto en GitHub y precisamente acaban de finalizar una nueva funcionalidad en la maáquina local y proceden a ejecutar los siguientes comandos para subir los al respositorio remoto

```bash
git add .
git commit -m "Añade nueva duncionalidad"
git push origin main
```
Sin embargo antes de ejecutar el "git push", se decide verificar que todo está en orden con la conectividad a internet y con el servidor de Git Hub.
## a) Realizar un análisis paso a paso del proceso completo, desde que se escribe el primer comando de verificación hasta que GitHub confirma la recepción de los cambios.
Para cada paso, usted deberá:

### - 1. Identificar la capa del modelo Osi involucrada principalmente en esa acción
### - 2. Mencionar los protocolos y estructuras de datos (tramas, paquetes, segmentos) que intervienen.
### - 3. Indicar qué comando (s) de red (de CMD de windows o herramientes como "ping", tracert, nslookup, netstat, pathping o incluso filtros de wireshark") podrian utilizar para verificar o diagnosticar problemas en ese paso especifico.
### - 4. Relacionar los conceptos de teletrafico (latencia, pérdida de paquetes, throughput) con el éxito o fracaso de la operación

Estructurar la respuesta siguiendo la secuencia lógica de eventos 

<img width="416" height="164" alt="image" src="https://github.com/user-attachments/assets/8b787516-abfe-4626-945c-76cf96a60da9" />

<img width="449" height="203" alt="image" src="https://github.com/user-attachments/assets/94b546a9-532b-47b7-9f47-43327787ec18" />

<img width="452" height="223" alt="image" src="https://github.com/user-attachments/assets/e0681ced-c5e8-47fe-a130-f09aaa0a92d0" />

<img width="419" height="214" alt="image" src="https://github.com/user-attachments/assets/72411c38-7c27-478a-902c-e20babb08a6e" />

# Respuesta
## Paso 1- Verificación de conectividad básica y resolución de nombres
### 1.¿Qué comando usaría para verificar conectividad IP con GitHub? ¿Qué capa OSI verifica y qué protocolo usa?

comando
```bash
ping github.com
```
- Capa OSI principalmente: capa 3 (red) porque verifica que se puede llegar por la IP al destino (aunque se apoya en capa 2 en la LAN)
- Protocolo que usa: ICMP

### 2.¿Cómo obtiene su equipo la IP de github.com? Proceso, protocolo, capa OSI y comando si falla.
El pc obtiene IP usando DNS:
 - El pc pregunta "¿Qué IP tiene github.com?"
 - El resolver DNS (normalmente el del router o ISP) responde con la IP

Protocolo: DNS (usa típicamente UDP 53, a veces TCP 53 si la respuesta es grande o para ciertas operaciones)

Capa OSI: Capa 7 (Aplicación) (DNS es un servicio de aplicación)

Si falla la resolución, esta el comando para diagnosticar manualmente

  ```bash
  nslookup github.com
  ```
  Tambien puede servir ipconfig /fludhdns para limpiar caché DNS si se sospecha de problema local.

  ### 3.Ping exitoso pero con latencia alta y variable: ¿qué métrica está afectada y cómo influye en git
  push?
  - Métrica afectada: Jitter (variación de la latencia) y tambien latencia alta.
  - ¿Coómo afecta a git push?
      - puede hacer que la conexion se sienta lenta, aumenta el tiempo de envio.
      - si la latencia/jitter es muy alta, puede haber timeouts, retransmisiones TCP y el push puede tardar mucho o fallar.

## Paso 2- Establecimiento de la conexión para el push (Git por HTTP/HTTPS)
### 1. ¿Qué protocolo de transporte abre conexión fiable?¿Qué mecanismo usa? Explicar "three-way hanshake"
- El protocolo de tranporte TCP es confiable.
- Mecanismo Three-way handshake:
   1. Cliente: servicodr: SYN (quiere iniciar conexión)
   2. Servidor: Cliente: SYN-ACK (Acepto y confirmo)
   3. Cliente: Servidor: ACK (Confirmo y queda establecida la conexión)

### 2. Ver segmentos TCP en tiempo real: herraienta y filtro (si ya se conoce la IP de GitHub)
Primero obtenemos la ip de GitHub desde el CMD o Powershell con el siguiente comando, tal y como se menciono anteriormente.

```bash
nslookup github.com
```
y en pantalla se vera la siguiente información

<img width="253" height="102" alt="image" src="https://github.com/user-attachments/assets/53811ea7-9007-4235-a7a9-cacf0fad092b" />

Procedemos abrir wireshark y elegir la interfaz correcta
En este caso la conexión es de WIFI, es decir, que seleccionamos esta opción para ver el trafico de datos.

<img width="553" height="431" alt="image" src="https://github.com/user-attachments/assets/d5633259-c5ff-4c5c-beef-95cb522ab29d" />

En el CMD realizamos ping a GitHub.com desde CMD y mientras este se ejecuta vemos el trafico de paquetes en Wireshark y filtramos con "ip.addr == 140.82.114.3 and tcp" y asi podemos observar lo siguiente:

<img width="956" height="500" alt="image" src="https://github.com/user-attachments/assets/eae5ae49-24df-43e9-91f4-5cea65747f0d" />

Con este filtro se esta mostrando solo el trafico HTTPS mediante el puerto 443 y el CMD podemos observar:
- latencia minima: 87ms
- macima: 122ms
- promedio: ~100ms

Ahora si ejecutamos el filtro sin el TCP podremos observar los paquetes ICMP

<img width="1012" height="737" alt="image" src="https://github.com/user-attachments/assets/f927f507-22cb-43de-90ec-1f5b04fc8b3c" />

Esto nos permite visualizar todo el trafico entre el equipo y els ervidor de GitHub.
En esta captura se observa la columan "Protocol" donde aparece ICMP y en la info muestra

- Echo (ping) request
- Echo (ping) reply

Y esto corresponde a los paquetes generados por el comando ping github.com

- Tu PC (172.20.10.2)  →  GitHub (140.82.114.3)   ICMP Echo Request
- GitHub (140.82.114.3) → Tu PC (172.20.10.2)     ICMP Echo Reply

Esto confirma que existe conectividad entre el equipo local y los servidores de Github.com

### 3. Puertos de origen y destino
En la cabecera tcp se observan dos puertos

1. puerto destino : 433 , este puerto corresponde al protocolo HTTPS, utilizado por Git para comunicarse con GitHub.
2. Puerto de origen; Este es un puerto efimero o dinamico, asignado temporalmente por el sistema operativo del cliente
   ejemplo: 64867 → 443

### Capa del modelo OSI
Los puertos TCP son gestionados por la Capa 4 (Transporte)

## Paso 3-Encapsulamiento y enrutamiento de los datos
### 1. Encapsulamiento desde Git hasta trama Ethernet + PDU por capa
Proceso:

1. Aplicación (GIT/HTTP/HTTPS): Genera los datos que se enviarán (contenido del push).
2. Transporte (TCP): Divide/organiza datos en segmentos, agrega puertos, números de secuencia, ACK, etc.
3. Enlace (Ethernet/WI.FI): Encasula en tramas, agrega MAC origen/destino y FCS.
4. Fisica: Se transmite como bits por el medio.

Nombre de la PDU por capa:
- Capa 7 (Aplicación): datos, por ejemplo "HTTP payload" / "datos de aplicación".
- Capa 4 (Transporte): Segmento TCP.
- Capa 3 (RED): Paquete IP
- Capa 2 (Enlace): Trama Ethernet.
- Capa 1 (Física): Bits.

### 2.Router congestionado y descarta paquetes: ¿cómo afecta git push, qué mecanismo TCP se activa, y qué comando identifica el salto con pérdida?

- ¿Cómo afecta al git push?
Se generan pérdida de paquetes, entonces TCP debe retransmitir, incluso el push tarda má o incluso puede fallar por timeouts.

- ¿Qué mecanismo TCP se activa?
Se activan las retransmisiones por falta de ACK y reduce la ventana (congestion de windosw), puede antrar en slow start o ajustar su tasa.

- ¿Qué comando ayudaa identificar en qué salto se pierden paquetes?
   -pathping github.com o pathping <IP_GITHUB> : ya que muestran la perdida por salto, es mejor que tracert para tener el punto de perdida mas claro, aunque tracert muestra la ruta, este cuantifica perdida como pathping.

### 3.En la cabecera IP, ¿qué campo evita que el paquete dé vueltas indefinidamente? Explicar
Campo: TTL (Time To Live) en IPv4 (IPv6 se llama Hop Limit).
Cada router reenvía el paquete reduce el TTL en 1, si este llega a 0, el paquete se descarta y se envía un IVMP "Time Exceeded"; El beneficio de esto es que vita bucles infiniros en caso de rutas mal configuradas.

## Paso 4- Confirmación y fin de la comunicación
### 1. ¿Qué mensaje TCP confirma recepción correcta? Relación con pérdida de paquetes y fiabilidadTCP confirma con ACK, si los ACK no llegan, TCP asume posible perdida y retransmite, por eso TCP es fiable asegurando la entrega usando ACK + retransmisiones + control de flujo o congestión.

### 2. ¿Cómo se cierra ordenadamente una conexión TCP?
Cierre típico en 4 pasos (FIN/ACK)
1. Cliente → Servidor: FIN
2. Servidor → Cliente: ACK
3. Servidor → Cliente: FIN
4. Cliente → Servidor: ACK
Así se asegura que ambos lados terminan de enviar datos antes de cerrar.

### 3. Monitorear el tráfico del push con SNMP: métricas y versión si se requiere cifrado
Métrica típicas en interfaces del router (MIB de interfaces):
- Bytes transmitidos/recibidos
- Paquetes recibidos/enviados
- Errores
- Paquetes descartados
- Estado de la interfacez
  
¿Qué versión SNMP usar si se necesita cifrado?
SNMPv3, porque soporta autenticación y cifrado (a diferencia de v2c que usa comunidad en texto plano).




