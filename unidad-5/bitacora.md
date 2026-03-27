# Unidad 5
ACTIVIDAD 1 --------------------------

El encapsulamiento, para mí, es una forma de proteger los datos dentro de una clase para que no puedan ser modificados directamente desde cualquier parte del programa. En lugar de eso, se accede a ellos mediante propiedades o métodos que permiten tener control sobre cómo se usan. Esto es útil, por ejemplo, cuando se quiere evitar que un valor importante cambie sin validación, como un nombre o algún dato clave dentro de un objeto.

La herencia es un mecanismo que permite que una clase reutilice atributos y métodos de otra clase. Sirve principalmente para evitar repetir código y organizar mejor el programa. Por ejemplo, se puede tener una clase base como “Animal” con características generales, y luego clases como “Perro” o “Gato” que heredan de esa clase y agregan sus propias particularidades.

El polimorfismo es la capacidad de que una misma referencia o método tenga diferentes comportamientos dependiendo del tipo de objeto que se esté utilizando. Es decir, se puede usar una misma instrucción, pero el resultado cambia según el objeto real.

<img width="813" height="72" alt="image" src="https://github.com/user-attachments/assets/271dca09-39ac-4f6c-8d3d-b18796c97afb" />

En el código proporcionado, un ejemplo claro de encapsulamiento es la línea private string nombre;, ya que este atributo no se puede acceder directamente desde fuera de la clase. En su lugar, se usa una propiedad pública llamada Nombre, que permite leer el valor pero controla cómo se puede modificar. Esto evita problemas como cambios no controlados desde otras partes del programa, ya que solo ciertas clases pueden modificar ese valor gracias al protected set.

<img width="751" height="432" alt="image" src="https://github.com/user-attachments/assets/1d033ded-0ad9-4bc4-804b-1fe7ec0afcf9" />

La herencia se puede ver claramente en la línea public class Circulo : Figura, donde la clase Circulo hereda de Figura. Esto significa que un objeto de tipo Circulo no solo tiene su atributo Radio, sino también el atributo Nombre que viene de la clase base. Lo mismo ocurre con Rectangulo.

En cuanto al polimorfismo, en el ciclo foreach se usa una variable de tipo Figura, pero esta puede contener tanto objetos Circulo como Rectangulo. Cuando se llama al método Dibujar(), el programa ejecuta la versión correcta dependiendo del tipo real del objeto. Mi idea de cómo funciona esto es que cada objeto guarda información sobre su tipo real, y en tiempo de ejecución el programa revisa ese tipo para decidir qué método ejecutar, sobre cómo se organiza esto internamente, me imagino que en memoria los datos se almacenan juntos en un mismo bloque. Por ejemplo, un objeto Rectangulo tendría algo como [Nombre | Base | Altura], donde primero están los datos de la clase base y luego los de la clase derivada.

Respecto al polimorfismo, creo que el programa tiene algún mecanismo interno para saber a qué método debe llamar. Tal vez cada objeto tiene una referencia o una especie de “tabla” que indica qué versión del método usar, y así cuando se llama a Dibujar(), se ejecuta la implementación correcta. 

En cuanto al encapsulamiento, considero que la restricción de acceso a los miembros private se revisa en tiempo de compilación. Es decir, si se intenta acceder a un atributo privado desde fuera de la clase, el compilador genera un error y el programa ni siquiera se ejecuta. Esto ayuda a prevenir errores antes de que el programa corra.

ACTIVIDAD 2 ----------------------------------------------

La aplicación implementa un sistema de partículas que simula algo similar a fuegos artificiales. El comportamiento general consiste en crear una partícula que sube desde la parte inferior de la pantalla y, después de cierto tiempo o al llegar a cierta altura, explota generando múltiples partículas nuevas con distintos patrones, el código está organizado usando programación orientada a objetos. Existe una clase base abstracta llamada Particle, la cual define el comportamiento general que deben tener todas las partículas. Esta clase declara métodos como update(), draw() e isDead(), que obligatoriamente deben ser implementados por las clases derivadas. También incluye métodos opcionales como shouldExplode(), getPosition() y getColor(), que permiten manejar comportamientos específicos como las explosiones.

<img width="834" height="521" alt="image" src="https://github.com/user-attachments/assets/1fab1c56-ea75-4e99-8293-903979718102" />

La clase RisingParticle representa la partícula inicial que sube. Esta tiene atributos como posición, velocidad, color, tiempo de vida y edad. En su método update(), la partícula se mueve en función de su velocidad, se incrementa su edad y se le aplica un efecto similar a la gravedad. Cuando la partícula alcanza cierta altura o supera su tiempo de vida, se marca como lista para explotar. En el método draw(), simplemente se dibuja como un círculo en pantalla.

Luego existe la clase ExplosionParticle, que funciona como base para las partículas que aparecen después de una explosión. Esta también maneja posición, velocidad, color, tamaño y tiempo de vida. Su comportamiento principal es moverse en distintas direcciones y desvanecerse con el tiempo, reduciendo su transparencia progresivamente.

A partir de esta clase base se crean tres tipos de explosiones. La clase CircularExplosion genera partículas que se mueven en direcciones distribuidas en un patrón circular, utilizando ángulos y funciones trigonométricas. La clase RandomExplosion asigna velocidades completamente aleatorias a cada partícula, generando un efecto más desordenado. Por último, la clase StarExplosion crea un patrón que simula una estrella, dibujando líneas en diferentes direcciones desde el centro, la clase principal ofApp es la encargada de manejar toda la aplicación. En el método setup() se configura la tasa de frames y el fondo de la pantalla. En el método update() se actualizan todas las partículas y se verifica si alguna debe explotar o eliminarse. Si una partícula debe explotar, se generan varias nuevas partículas de tipo explosión en la misma posición y con el mismo color. Luego, la partícula original se elimina del vector para evitar que siga existiendo en memoria. También se eliminan las partículas que ya han terminado su ciclo de vida.

<img width="802" height="835" alt="image" src="https://github.com/user-attachments/assets/ebb73ab6-f2fd-4cf3-9a7a-5df39ead4924" />

El método draw() recorre todas las partículas y las dibuja en pantalla. La función createRisingParticle() se encarga de crear nuevas partículas iniciales con valores aleatorios en posición, dirección, color y tiempo de vida, lo que genera variedad en la simulación, cuando el usuario hace clic con el mouse se crea una nueva partícula. Si se presiona la barra espaciadora, se generan muchas partículas al mismo tiempo, lo que produce múltiples explosiones simultáneas. Además, al presionar la tecla “s” se guarda una captura de pantalla, por ultimo, el destructor de la clase ofApp se encarga de liberar la memoria eliminando todas las partículas que aún existan, lo cual es importante porque se están usando punteros dinámicos.

<img width="795" height="238" alt="image" src="https://github.com/user-attachments/assets/f518574b-09ba-43ae-9a83-600703e19204" />


En conjunto, este programa demuestra el uso de herencia, ya que todas las partículas derivan de una clase base; polimorfismo, porque todas las partículas se manejan mediante el mismo tipo pero ejecutan comportamientos diferentes; y encapsulamiento, porque cada clase administra sus propios datos internos. También se evidencia el uso de estructuras dinámicas como std::vector y el manejo manual de memoria con new y delete.

<img width="1425" height="933" alt="image" src="https://github.com/user-attachments/assets/67f3ed29-fa93-494c-8900-5f003cc7a125" />

ACTIVIDAD 3 ---------------------

(Modificando un poco el codigo de ofApp,cpp y ofApp.h)

Antes de ejecutar el programa, esperaba que un objeto en memoria fuera simplemente un conjunto de datos organizados, como sus atributos (pos, life, etc.). También pensaba que cada objeto tendría sus propias funciones almacenadas directamente dentro de él.

<img width="1905" height="541" alt="image" src="https://github.com/user-attachments/assets/65f1bede-61d3-478c-b556-5baf56243b95" />

Observación del objeto ofApp: Al ejecutar el programa y usar el depurador, encontré el objeto ofApp a través de this en la ventana Locals. Se pudo observar que: Contiene un vector llamado particles, Este vector almacena punteros a objetos, no los objetos directamente

Observación de CircularExplosion: Al inspeccionar un objeto de tipo CircularExplosion, se observó que en memoria contiene: Primero: un puntero oculto (_vtable o _vptr), Luego: sus atributos (pos, life)

<img width="900" height="473" alt="image" src="https://github.com/user-attachments/assets/7ad4682d-6f2f-4bc8-933c-329b92600991" />

Se analizó cómo está construido el objeto en memoria y se observó que CircularExplosion hereda de Particle. Al inspeccionarlo en el depurador, se puede ver que primero aparece en memoria la parte correspondiente a la clase base (Particle) y después los atributos propios de CircularExplosion, como la posición y el tiempo de vida. Esto permite concluir que los objetos derivados contienen internamente la información de la clase base como primera parte, lo cual explica cómo funciona la herencia a nivel de memoria en C++. Al observar el objeto en el depurador también se encontró que el primer valor en memoria no es un atributo como tal, sino un puntero a la tabla de funciones virtuales, conocido como _vtable (o _vptr). Esta tabla contiene las direcciones de memoria de las funciones virtuales, como update, draw e isDead.

Cuando se compararon objetos de tipo CircularExplosion y StarExplosion, se vio que ambos tienen una _vtable, pero no apuntan al mismo lugar. Cada uno tiene su propia tabla con direcciones distintas, ya que cada clase implementa sus propias versiones de los métodos virtuales. Esto es importante porque permite que, aunque ambos objetos se manejen como Particle*, el programa sepa cuál función debe ejecutar en cada caso. A partir de esto se concluye que la _vtable permite que el programa decida en tiempo de ejecución qué método llamar dependiendo del tipo real del objeto. Esto es lo que se conoce como polimorfismo.

Esto se puede relacionar con el ejemplo visto en C#, donde se utiliza una interfaz IAnimal. En ese caso, tanto Perro como Gato se manejan como IAnimal, pero cada uno ejecuta su propio método HacerSonido. En C++ ocurre algo similar: todos los objetos se almacenan como Particle*, pero cada uno ejecuta su propio draw() gracias a la _vtable.

La tabla de funciones virtuales sirve entonces para permitir el polimorfismo, ejecutar el método correcto según el tipo real del objeto y evitar el uso de múltiples condicionales para diferenciar comportamientos.

<img width="544" height="585" alt="image" src="https://github.com/user-attachments/assets/d0baf09e-64d6-43a2-9af1-178461777737" />
<img width="458" height="583" alt="image" src="https://github.com/user-attachments/assets/986f16c5-9bdc-455a-909a-a171bddb6087" />


El código tuvo que modificarse ligeramente para poder cumplir con la actividad y facilitar el análisis en el depurador. Se creó una clase base Particle con métodos virtuales, y a partir de esta se definieron las clases CircularExplosion y StarExplosion. También se utilizó un vector<Particle*> para poder almacenar diferentes tipos de objetos bajo un mismo tipo base, aplicando así el polimorfismo. Además, se añadieron objetos tanto en el método setup() como mediante interacción con el mouse, para asegurar que existieran instancias en memoria que pudieran ser inspeccionadas durante la ejecución.


ACTIVVIDAD 4 --------------------------
