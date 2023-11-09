## Planteamiento del problema

Una asociación sin ánimo de lucro de asistencia a personas con dependencia o movilidad reducida, presta todos los días servicio de cuidados y atención por las mañanas de 08:00 a 14:00.

Gracias a una extensa red de voluntarios que se ofrecen a realizar el servicio según las necesidades de los usuarios, el servicio está garantizado.

Cada día, para conocer las necesidades y lo disoponible, los usuarios solicitan el servicio de cuidados y los voluntarios marcan su disponibilidad.

A las 7:00 de la mañana los voluntarios reciben un mensaje con los datos de la persona que deben de atender ese día.

Simplificando el problema, el coste para prestar este servicio para la ONG se puede dividir en gastos fijos (Alquiler, luz, agua, material fungible, etc...) y gastos variables (pago de dietas y desplazamiento del voluntariado).

Quitando la parte del coste fijo y de las dietas que depende del número de usuarios que solicitan el servicio, el único concepto que pueden gestionar es el gasto en desplazamientos.

El objetivo es encontrar la asignación del personal voluntariado más económica.

## Modelización del problema
Para modelizar el problema como un problema de tipo QUBO, llamamos $u_i$ a cada uno de los usuarios, $v_i$ a cada voluntariado, $d_
{ij}$ la distancia que recorre el voluntario $v_i$ para llegar a casa del usuario $u_j$.

Cada día marcamos con el valor 1 a los usuarios que han solicitado atención y con 0 en caso contrario.
De la misma manera, marcamos con 1 a los voluntarios que han indicado su disponibilidad y con 0 en caso contrario.

Por último denotamos por $x_{ij}$ la variable que vale 1 si el voluntario $v_i$ ha ido a atender al usuario $u_j$.

De esta forma la distancia que se ha recorrido en un día para cubir el servicio es

$\sum_{i=1}\ \sum_{j=1}\ d_{ij}\ u_i\ v_j\ x_{ij}$

Con las siguiente restriciones:
* Un voluntario solo puede atender a un usuario
  $\sum_{j=1}\ x_{ij}\ =\ v_i$
* Un usuario que no solicita el servicio no puede recibir un voluntario
  $\sum_{i=1}\ x_{ij}\ =\ u_j$
* Todas las peticiones tienen que ser atendidas
  $\sum_{i=1}\ \sum_{j=1}\ x_{ij}\ =\ \sum_{i=1} u_j$

De esta manera la función QUBO a minimizar es
$f(x)= \sum_{i=1}\ \sum_{j=1}\ d_{ij}\ u_i\ v_j\ x_{ij} + (\sum_{j=1}\ x_{ij}\ -\ v_i)^2 + (\sum_{i=1}\ x_{ij}\ -\ u_j)^2 + (\sum_{i=1}\ \sum_{j=1}\ x_{ij}\ =\ \sum_{i=1} u_j)^2$

Desarrollamos la expresión y obtenemos
