### Comparacion de robots

| Característica | Motoman MH6 | ABB IRB140 |
| ------------- | ------------- | ------------- |
| Fabricante | Yaskawa | ABB |
| Tipo de robot | Articulado | Articulado |
| Número de ejes | 8* | 6 |
| Carga máxima | 10 kg | 6 kg |
| Alcance horizontal | 1422 mm | 810 mm |
| Repetibilidad | ±0,08 mm | ±0,03 mm |
| Masa | 130 kg | 98 kg |

En lo que respecta a aplicaciones ambos robots trabajan en ámbitos similares, siendo estos aplicaciones industriales que requieren flexibilidad de alcance y herramientas, posiciones de entradas variables y cargas pequeñas o moderadas. Una diferencia particular es la forma en la que ambos robots han sido modificados durante su tiempo en la universidad, particularmente que el Motoman ha sido modificado con otros añadidos durante su tiempo en la sala CAM, el septimo grado de libertad que tiene es para un manipulador lateral y el octavo controla un mecanismo para desplazar el manipulador entero.
### Posiciones de Home

Home 1 y Home 2 son las 2 posiciones de descaso que tiene el Robot, ambas orientadas que el manipulador regrese a ellas y que pase la mayor parte de su tiempo así. La diferencia esta en la escala de operación: Home 2 es la posición que tima el manipulador cuando esta en operación pero no esta tomando alguna accion en particular, es una posición a desde la que las articulaciones deben ejercer comparativamente poco tiempo y energía para llegar a los que les pidan las rutinas creadas por el usuario, al menos en posiciones que no sean extremadamente exoticas, es en efecto un punto coun al que el manipulador puede volver.
<div align="center">
  <img width="285" height="337" alt="Posicion Home1" src="./Home1.jpg" />
  <img width="285" height="337" alt="Posicion Home2" src="./Home2.jpg" />
</div>

Por otro lado el punto Home 1 es la posición de descanso del manipulador, en este punto el gasto de energía para mantener posición es efectivamente nulo, lo que permite que los frenos experimenten un desgaste mucho menos, demás el volumen conjunto del robot también es menor, lo que facilita el transporte en conjunto. Esta es la posición es mejor para cuando el robot esta apagado por una razón u otra.

Dada esta informacion la mejor posicion para la operacion del manipulador es Home 2, con el entendimiento de que se llegara a Home 1 antes de que se apague el Robot.

### Movimientos Manuales del Robot

Los movimientos manuales del Robot son realizados via su teach pendant (aclaracion, el teach pendant de la imagen es el mismo modelo del que esta en la sala CAM pero no es exactamente ese).

<div align="center">
  <img width="285" height="337" alt="aleramirezgo" alt="Teach Pendant para el robot (mismo modelo pero no el que esta en sala CAM)" src="./tpYaskawa.jpg" />
</div>

Para operar el robot de forma manual es necesario prenderlo primero (verificar que los reles pertinentes esten prendidos, que el controlador este alimentado, colocar los diales donde deben estar, etc), luego se verifica que la llave este en el modo TEACH, seleccionar el modo de movimiento por articulaciones en la pantalla, y finalmente mover la articulación que se desee usando los botones del teach pendant. Para cambiar al espacio de trabajo se vuelve a la pantalla y se elige ese modo y el sistema de coordenadas que se va a utilizar (de flanche, TPC o de base) y otra vez se pasa a los botones para mover el robot

### Comunicación RoboDK-Motoman
1. El computador ejecuta RoboDK.
2. El computador establece conexión con el controlador del robot, comprobado via pingeo.
3. El controlador recibe las instrucciones de movimiento.
4. El controlador verifica las condiciones necesarias para ejecutar las órdenes.
5. Los servomotores accionan las articulaciones.
6. El robot realiza el movimiento solicitado.
7. El sistema devuelve información de posición y estado cuando el protocolo lo permite, dando señal de movimiento constante mediante el Teach Pendant.

###Robo DK

RoboDK es un entorno multi-marca de simulación y programación fuera de línea que permite montar la celda robótica en 3D, comprobar que no existan colisiones ni singularidades, diseñar trayectorias complejas (como la trayectoria polar del laboratorio mediante su interfaz o código en Python), generar programas en lenguaje nativo INFORM (.JBI) y controlar el robot en vivo desde el computador. La comunicación entre el PC y el controlador del Motoman MH6 se realiza a través de una red local Ethernet (TCP/IP) con cable de red y direcciones IP dentro de la misma subred, empleando el protocolo High-Speed Ethernet (HSE) de Yaskawa y el driver específico de Motoman (apiv2) mientras el controlador está en modo REMOTE. Cuando se ejecuta la rutina en línea ("Run on Robot"), RoboDK toma cada coordenada cartesiana de la trayectoria, calcula mediante cinemática inversa los ángulos que deben adoptar los seis ejes del brazo, divide el recorrido en puntos intermedios (waypoints) y los envía secuencialmente por red al controlador. A medida que los motores avanzan, el controlador devuelve la lectura real de los encoders al computador para sincronizar el modelo 3D en pantalla con el movimiento físico hasta completar toda la trayectoria

### Comparacion RoboDK y Robotstudio

RobotStudio es en primer lugar un software para productos ABB, eso lo deja mas por debajo en términos de versatilidad, pero a cambio gana profundidad en los robots que utiliza, así como precisión vía los códigos en RAPID, en particular la modalidad de pasar código desde la simulación a RAPID y viceversa es maravilloso a la hora de iterar procesos, tambien es mas complicado de utilizar y pide proyectos en carpetas para funcionar correctamente.

RoboDK a cambio es mucho mas simple, permite traer una gran variedad de productos de varias marcas y ofrece la modalidad compartida de simulación por bloques y el uso de Python, un lenguaje mucho mas general y con mayor cantidad de librerías disponibles, dando opciones directas para la creación de puntos y caminos que requerían soluciones creativas o trabajo intenso en RobotStudio, también da los proyectos en archivos unicos.

En lo personal apoyo mas a RobotStudio en virtud de que los problemas de licencia fueron menores.

### Diagrama de flujo

<div align="center">
  <img width="285" height="337" alt="Diagrama de flujo" src="./Diagrama de flujo.jpg" />
</div>

### Codigo de la simulacion
El codigo fue subido de forma independiente como "prog2.txt".
### Video de simulación y prueba
Link del video de demostracion: https://www.youtube.com/watch?v=zOlbh4mJVK8
