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
