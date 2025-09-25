# Actividad-de-Refuerzo
Solución de la actividad de refuerzo 2.3
## DESCRIPCIÓN
Esta actividad consiste en el diseño de un sitema que sea capaz de "medir" el nivel de un tanque de agua por medio de unos contactos que se cierran dependiendo de el nivel de un liquido, toda la actividad desarrollada a continuacion utiliza logica ladder para el diseño de este sistema, se utilizo Codesys para la creacion de una HMI que simula el funcionamiento de el circuito montado en hardware cuyo programa fue creado en OpenPLC con el mismo diagrama ladder que se utilizo en Codesys para el desarrollo de el HMI.
## PROCESO DE DISEÑO
Lo primero es entender los estados por los que pasa el sistema y que condiciones se tienen que cumplir para que cambie de estado, en este caso se diseño teniendo en cuenta cuatro posibles estados:
1- Empty el cual seria la ausencia de liquido.
2- Low Level el cual seria cuando hay suficiente liquido para que se cierre el primer contacto.
3- Optimal Level el cual sucederia cuando hay suficiente liquido para que se cierre el segundo contacto.
4- Overflow el cual sucederia cuando el nivel de liquido esta en el limite y cierra el tercer contacto.

Lo siguiente es entender bajo que logica necesita funcionar el sistema, esto significa que por ejemplo no se puede activar en el HMI la alerta de overflow si low level u optimal level estan abiertos ya que no estaria lleno el tanque ya que estos contactos deberian estar cerrados si el tanque ya esta lleno. Esta logica se aplica a los tres contactos funcionando de la siguiente manera:

-Para detectar al primer estado del sistema (Empty_tank) se utiliza un contacto normalmente cerrado de la entrada llamada low_level lo que quiere decir que mientras esa entrada no se active la luz del HMI que representa este estado estara apagada.

-En el segundo estado (Low_level_tank) depende de un contacto que tambien depende de la entrada low_level al esta entrada ser TRUE cierra el primer contacto, adicionalmente tiene un contacto normalmente cerrado que depende de la entrada optimal_level, ambos contactos estan puestos para formar una estructura AND por lo que se tienen que cumplir ambas condiciones, un True de la entrada low_level y un FALSE de la entrada optimal level. 

-El el tercer estado (Optimal_level_tank) sigue una estructura similar solo que en este caso ambas entradas low_level y optimal_level dependen de contactos abiertos y el ultimo contacto es normalmente cerrado tambien puesto para formar una estructura AND y depende de la entrada overflow mientras esta este en el estado FALSE activara este tercer estado.

-El ultimo estado (Overflow_tank) depende de tres contactos que a su vez depende de las tres entradas anteriormente mencionadas low_level, optimal_level y overflow.

Por ultimo se diseño la interfaz HMI en codesys las cual cosiste de 4 luces de colores distintos siendo azul la que avisa de que el tanque esta vacio, amarillo la que avisa que el nivel de liquido es bajo, verde la que avisa que el nivel de liquido es optimo y rojo para avisar que el nivel de liquido esta rebasando la capacidad del tanque odsea el estado de overflow, a su vez hay tres palancas que manejan el estado de las tres entradas que posee el sistema (low_level, optimal_level y overflow) para asi representar de manera correcta el sistema

### Imagen del HMI en codesys

<img width="560" height="303" alt="image" src="https://github.com/user-attachments/assets/ac7f5d01-3b56-40a6-bec6-11b5bed4adfb" />

## ESQUEMAS

### Esquema Ladder (estado empty)

<img width="558" height="156" alt="image" src="https://github.com/user-attachments/assets/7eacdbf8-6d53-4aa3-90aa-8db0cbf91f0f" />

### Esquema Ladder (estado low level)

<img width="568" height="177" alt="image" src="https://github.com/user-attachments/assets/1ee43855-664e-4949-8776-e8e61cc0667e" />

### Esquema Ladder (estado optimal level)

<img width="563" height="177" alt="image" src="https://github.com/user-attachments/assets/22541d1f-7928-46df-a14d-1dc4338a4fcc" />

### Esquema Ladder (estado overflow)

<img width="542" height="169" alt="image" src="https://github.com/user-attachments/assets/88947a10-db1a-4558-b98a-9e08ed0ce737" />

### Esquema de conexiones fisicas
<img width="1169" height="827" alt="Schematic_Control-de-Tanques_2025-09-24" src="https://github.com/user-attachments/assets/f230a304-b695-4c6b-b36d-15f5faae99b0" />
