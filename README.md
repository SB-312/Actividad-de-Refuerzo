# Actividad-de-Refuerzo
Solución de la actividad de refuerzo 2.3
## Descripcion
Esta actividad consiste en el diseño de un sitema que sea capaz de "medir" el nivel de un tanque de agua por medio de unos contactos que se cierran dependiendo de el nivel de un liquido, toda la actividad desarrollada a continuacion utiliza logica ladder para el diseño de este sistema, se utilizo Codesys para la creacion de una HMI que simula el funcionamiento de el circuito montado en hardware cuyo programa fue creado en OpenPLC con el mismo diagrama ladder que se utilizo en Codesys para el desarrollo de el HMI.
## Proceso de Diseño
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
