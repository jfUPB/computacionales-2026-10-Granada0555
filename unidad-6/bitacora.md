# Unidad 6
-----------------------------------------------  ACTIVIDAD 1  ------------------------------------------------

¿Qué observas en la aplicación al presionar las teclas a, r, s, n?

Al presionar "a" observamos como las particulas se acercan (atraen) y siguen el cursor del mouse
Al presionar "r" observamos como las particulas se alejan (son repelidas) por el cursor del mouse a donde sea que el vaya 
Al presionar "s" observamos como las particulas se quedan estaticas (se detienen en donde esten)
Al presionar "n" observamos como las particulas cambian de direccion de movimiento aleatoriamente

<img width="1070" height="823" alt="Captura de pantalla 2026-04-10 162624" src="https://github.com/user-attachments/assets/ee25689e-2ebd-4ebc-aecd-ed48a4eaf750" />
<img width="983" height="748" alt="Captura de pantalla 2026-04-10 162557" src="https://github.com/user-attachments/assets/8d34e114-ed21-4c87-bb47-219c508e98c6" />
<img width="1910" height="1026" alt="Captura de pantalla 2026-04-10 161954" src="https://github.com/user-attachments/assets/080e86cc-f6e9-4aa4-9616-203885c596f7" />
<img width="1019" height="756" alt="Captura de pantalla 2026-04-10 162651" src="https://github.com/user-attachments/assets/289320ef-29ef-4004-9f09-fe52f91f1ff5" />

¿Qué diferencias notas entre los tipos de partículas?

Cada particula tiene colores, tamaños y velocidades distintas entre si

<img width="1028" height="798" alt="image" src="https://github.com/user-attachments/assets/895e1432-5f9f-4192-9f56-38825699ff0f" />

¿Cómo crees que el código organiza la comunicación entre las teclas, las partículas y el cambio de comportamiento?

El código organiza la comunicación de una forma bastante clara separando quién envía la información, quién la recibe y cómo se comportan las partículas, cuando el usuario presiona una tecla, lo único que hace la aplicación es enviar un mensaje general (por ejemplo “attract”, “repel”, etc.). No controla directamente a cada partícula, sino que lanza ese evento para todas. Las partículas están registradas para recibir esos mensajes, así que cuando se envía uno, cada partícula lo recibe automáticamente. Al recibirlo, cada una decide qué hacer: cambia su estado según el evento recibido. Ese estado es lo que define su comportamiento. Es decir, la partícula no cambia solo un valor, sino que cambia completamente la forma en la que se mueve. Por ejemplo, puede pasar a seguir el mouse, alejarse, detenerse o moverse de forma aleatoria. En resumen, las teclas envían mensajes, las partículas los reciben y, a partir de eso, cambian su estado, lo que modifica su comportamiento en la simulación.


-----------------------------------------  ACTIVIDAD 2  ----------------------------------------------

<img width="1910" height="1102" alt="image" src="https://github.com/user-attachments/assets/4ceefd0e-97a3-44b0-bc8a-9f4d2d418da5" />

<img width="1906" height="1083" alt="image" src="https://github.com/user-attachments/assets/ab47850e-5dc1-4a34-a4e7-c3b5c47d0d28" />

Coloqué el breakpoint dentro de la función Subject::notify, específicamente en el ciclo for, porque en este punto el sujeto recorre todos los observadores y les envía la notificación. Es un lugar clave para observar cómo el patrón Observer se ejecuta en tiempo real. Al ejecutar el programa y presionar una tecla, el depurador se detuvo en el breakpoint. En las variables locales se pudo observar que la variable event tenía el valor "stop" y que existía un vector llamado observers con varios elementos. Cada uno de estos elementos correspondía a una dirección de memoria, lo que indica que son punteros a objetos y no objetos directamente. Esto demuestra el funcionamiento del patrón Observer, ya que el Subject mantiene una colección de observadores mediante referencias en memoria y los recorre para enviarles notificaciones. No necesita conocer los detalles internos de cada objeto, solo sus direcciones, lo que permite que el sistema esté desacoplado y sea más flexible.


<img width="1887" height="819" alt="image" src="https://github.com/user-attachments/assets/f15e6438-7b43-4941-8507-4c8c584a0b41" />

Coloqué un breakpoint en la función Particle::onNotify, ya que este es el punto donde cada observador recibe la notificación enviada por el Subject. Es un lugar clave porque permite identificar qué objeto específico está siendo llamado durante la ejecución. Al ejecutar el programa y entrar en esta función con el depurador, se pudo observar la variable this, la cual representa el objeto actual que está recibiendo la notificación. Esta variable contiene una dirección de memoria (por ejemplo: 0x00000123...). Al comparar esta dirección con las que aparecían previamente en el vector observers dentro de Subject::notify, se pudo verificar que coincide exactamente con una de ellas. Esto permite concluir que el Subject sabe a quién notificar porque almacena directamente las direcciones de memoria de los observadores. Cuando ocurre un evento, recorre ese vector y llama a los métodos de esos mismos objetos, utilizando esas referencias. De esta manera, no necesita identificar a los observadores por nombre o tipo, sino que trabaja directamente con sus direcciones en memoria, lo que confirma el funcionamiento del patrón Observer.


<img width="1873" height="856" alt="image" src="https://github.com/user-attachments/assets/734a0801-4d01-42d2-890a-0e4fd2328256" />

Coloqué un breakpoint en la función Particle::setState, ya que este es el punto donde se realiza el cambio de estado de cada partícula. Este lugar es clave para observar cómo el patrón State modifica el comportamiento del objeto en tiempo de ejecución. Al ejecutar el programa y presionar una tecla, el depurador se detuvo en el breakpoint. En las variables locales se observó el puntero state, el cual contiene una dirección de memoria que representa el estado actual del objeto. Al avanzar una línea en el código, se pudo ver que esta dirección cambia, lo que indica que el estado anterior fue reemplazado por uno nuevo. Este comportamiento demuestra que el objeto no cambia su estructura, sino que cambia el objeto interno que define su comportamiento. El estado anterior deja de existir porque es gestionado mediante unique_ptr, lo que asegura que se libere automáticamente cuando se asigna uno nuevo. Esto confirma el funcionamiento del patrón State, ya que permite cambiar el comportamiento de un objeto dinámicamente mediante la sustitución de su estado interno.

<img width="1907" height="1063" alt="image" src="https://github.com/user-attachments/assets/afa3329f-e370-44f0-9777-5ee009e48db7" />

Coloqué breakpoints en las funciones NormalState::update y AttractState::update, ya que estas representan diferentes comportamientos posibles de una misma partícula dependiendo de su estado. Este punto es clave para observar cómo el patrón State utiliza polimorfismo para cambiar el comportamiento en tiempo de ejecución. Al ejecutar el programa y presionar la tecla n, el depurador se detuvo en la función NormalState::update, lo que indica que la partícula se encuentra en estado normal. Posteriormente, al presionar la tecla a, el flujo del programa se dirigió a la función AttractState::update, mostrando un comportamiento distinto. Esto demuestra que, aunque el código trabaja con un puntero genérico de tipo State, en tiempo de ejecución se llama a la implementación específica correspondiente al estado actual del objeto. Este mecanismo se basa en el polimorfismo y el despacho dinámico, permitiendo que el comportamiento cambie sin modificar la estructura del objeto. De esta manera, el patrón State logra que un mismo objeto tenga diferentes comportamientos dependiendo de su estado interno.


<img width="1909" height="1104" alt="image" src="https://github.com/user-attachments/assets/3e111642-35e6-4182-a038-66e0db42f8e8" />

<img width="1911" height="702" alt="image" src="https://github.com/user-attachments/assets/f2ca3397-0efc-4815-8b5b-d6a08a1745ed" />

<img width="1909" height="1029" alt="image" src="https://github.com/user-attachments/assets/87330fff-c502-418b-a3bb-3d6548477d8d" />

Coloqué un breakpoint en la función ParticleFactory::createParticle, ya que este es el punto donde se crean los objetos de tipo Particle. Esto permite observar cómo la factory genera instancias dependiendo del parámetro recibido. Al ejecutar el programa, el depurador se detuvo en esta función y se pudo observar el parámetro type, que indicaba el tipo de partícula a crear. Al avanzar en la ejecución hasta el retorno, se identificó que la función devuelve un puntero con una dirección de memoria específica, correspondiente al objeto recién creado. Posteriormente, se colocó un breakpoint en ofApp::setup, justo después de insertar las partículas en el vector particles. Al inspeccionar este vector, se observó que las direcciones de memoria de sus elementos coinciden con las direcciones de los objetos creados por la factory. Esto demuestra que la factory es la encargada de crear los objetos y que estos mismos son almacenados y utilizados posteriormente en el programa. El patrón Factory permite centralizar la creación de objetos, desacoplando el proceso de instanciación del resto del código y facilitando la extensión del sistema.



------------------------------------------------- ACTIVIDAD 3 -------------------------------------------------------



<img width="1040" height="646" alt="image" src="https://github.com/user-attachments/assets/513a0c50-9021-4a49-bc2d-cc84e08215d4" />

El diagrama muestra el flujo completo de una acción del usuario desde que se presiona una tecla hasta que cambia el comportamiento de las partículas. Todo comienza en keyPressed dentro de ofApp, donde se detecta la entrada del usuario. A partir de ahí, se llama a notify, el cual pertenece al Subject, encargado de comunicar el evento a todos los observadores registrados. Esta parte representa el patrón Observer, ya que el sujeto no conoce directamente a las partículas, sino que simplemente recorre una lista de referencias y notifica a cada una mediante onNotify. Cada partícula recibe el evento en onNotify y, dependiendo de la tecla presionada, llama a setState, donde cambia su estado interno. En este punto entra en juego el patrón State, ya que el objeto no cambia su estructura, sino que reemplaza el objeto de estado que define su comportamiento. Esto provoca que, en las siguientes llamadas a update, se ejecute una implementación diferente gracias al polimorfismo y al uso de la tabla virtual (_vtable), lo que permite cambiar dinámicamente la lógica de cada partícula.

Por otro lado, el patrón Factory ya cumplió su función en la fase de inicialización (setup), donde se crean las partículas. Su rol es centralizar la creación de objetos y desacoplar este proceso del resto del sistema, permitiendo instanciar diferentes tipos de partículas sin modificar el código principal. Si no se utilizara el patrón Observer, el flujo cambiaría significativamente. En lugar de usar notify, ofApp tendría que recorrer directamente todas las partículas y asignarles su nuevo estado. Esto aumentaría el acoplamiento entre ofApp y las partículas, ya que el controlador principal tendría conocimiento directo de todos los objetos y su comportamiento. Además, el diagrama se simplificaría en apariencia, pero el diseño sería menos flexible y más difícil de mantener, ya que cualquier cambio en la lógica de las partículas implicaría modificar también la clase principal.



--------------------------------------------   ACTIVIDAD 4   ------------------------------------------------------------


Evidencia 1 ----------------------

<img width="1903" height="944" alt="image" src="https://github.com/user-attachments/assets/9f642032-a11a-4145-bd45-c03ad533d923" />

Al ejecutar el programa con el breakpoint en la factory, se observa que el valor de type es "comet", por lo que se entra a esa rama del condicional. Esto confirma que el nuevo tipo de partícula está siendo reconocido correctamente por el sistema, al inspeccionar el objeto Particle* p recién creado, se puede ver que sus atributos fueron modificados según lo definido: el tamaño (size) es mayor (8), el color cambia a un tono naranja (ofColor(255, 100, 0)), y la velocidad es multiplicada, lo que hace que la partícula se mueva más rápido que las normales. Esto demuestra que la factory no solo crea objetos, sino que también los configura dependiendo del tipo, cumpliendo correctamente su rol en el diseño.

Evidencia 2 -----------------------

<img width="1864" height="779" alt="image" src="https://github.com/user-attachments/assets/56de3e9c-cfa6-409c-8917-7e5ff257f82e" />

Al activar el estado PulseState y observar el puntero state en el debugger, se puede ver que apunta a un objeto de tipo diferente al de NormalState. Al inspeccionar la _vtable asociada a ese objeto, se evidencia que las direcciones de las funciones virtuales cambian, especialmente la función update.

<img width="712" height="600" alt="image" src="https://github.com/user-attachments/assets/314d7529-b5d3-4bd9-9572-945e2e08caf7" />

<img width="1786" height="795" alt="image" src="https://github.com/user-attachments/assets/ce443114-0d1a-43cd-9942-d07244bea211" />

Posteriormente, se repitió el mismo procedimiento con una partícula en estado NormalState. Al comparar ambas _vtable, se evidenció que las direcciones almacenadas en las posiciones [0], [1], [2], etc., son diferentes entre los dos estados. Esto ocurre porque cada clase que hereda de State tiene sus propias implementaciones de las funciones virtuales (como update o draw), por lo que el compilador genera una _vtable distinta para cada tipo. En consecuencia, el puntero _vptr cambia dependiendo del estado activo, permitiendo que el comportamiento de la partícula se resuelva dinámicamente en tiempo de ejecución.

Evidencia 3 ----------------------

<img width="1912" height="776" alt="image" src="https://github.com/user-attachments/assets/93af28e7-1fbd-490b-9012-844960c4f20d" />

<img width="1897" height="719" alt="image" src="https://github.com/user-attachments/assets/86992d2c-0588-4a98-8bd5-0d0fc579e177" />

<img width="1907" height="636" alt="image" src="https://github.com/user-attachments/assets/dacff866-7b62-4ab1-bbad-d15a6eeeb58f" />

<img width="1910" height="682" alt="image" src="https://github.com/user-attachments/assets/c26ae4a5-d9f0-482f-9f75-1d9b31f23838" />

Elección del punto de inspección

Se colocaron breakpoints en cuatro puntos clave del programa:

keyPressed, donde se genera el evento al presionar una tecla
notify, donde se distribuye el evento a los observadores
onNotify, donde cada partícula recibe el evento
setState, donde finalmente se cambia el estado

Estos puntos permiten seguir paso a paso cómo viaja el evento "pulse" dentro del sistema. Al ejecutar el programa y presionar la tecla 'p', el flujo observado en el depurador fue el siguiente: Primero, en keyPressed, se detecta la tecla presionada (valor 112, correspondiente a 'p') y se llama a notify("pulse"). Luego, en notify, el evento "pulse" se recorre a través del vector de observadores, enviándose a cada partícula mediante onNotify. Después, en onNotify, cada partícula evalúa el valor del evento. Cuando el evento es "pulse", se ejecuta la condición correspondiente y se llama a setState(new PulseState()). Finalmente, en setState, el puntero state de la partícula se actualiza para apuntar a una nueva instancia de PulseState, cambiando así su comportamiento, esto confirma que el patrón Observer está funcionando correctamente. El método keyPressed no modifica directamente las partículas, sino que emite un evento general. Luego, notify se encarga de distribuirlo, y cada partícula decide cómo reaccionar de forma independiente en onNotify. El cambio de estado ocurre de forma encapsulada en setState, lo que mantiene el código organizado y desacoplado.

Evidencia 4 -------------------------
Se decidió que el nuevo estado PulseState herede directamente de la clase base State, en lugar de heredar de otro estado existente como NormalState

<img width="1919" height="1048" alt="image" src="https://github.com/user-attachments/assets/19ebf3c4-8f22-4be7-98b5-754f48fbb531" />

PulseState tiene un comportamiento propio que no corresponde a una simple variación de los otros estados. En este caso, modifica el tamaño de la partícula de forma oscilante y cambia su color al entrar en el estado, lo cual no depende del comportamiento de estados como NormalState, AttractState o RepelState.
Por esta razón, se consideró más adecuado que herede directamente de State, definiendo su propia lógica sin depender de implementaciones intermedias.


<img width="1910" height="718" alt="image" src="https://github.com/user-attachments/assets/bbdfd39a-849d-4ba7-bca0-43f6bab72380" />

Durante la ejecución, se colocó un breakpoint en setState. Al presionar la tecla 'p', se observó que el puntero newState apunta a una instancia de PulseState. se verificó que el puntero state de la partícula cambia a una dirección de memoria correspondiente a un objeto de tipo PulseState. Además, al continuar la ejecución, se comprobó que el método update ejecutado corresponde al de PulseState, ya que la partícula comienza a cambiar de tamaño de forma periódica, lo cual no ocurre en otros estados. Finalmente esta decisión permite mantener un diseño más claro y modular, ya que cada estado define su propio comportamiento sin depender de otros. Si PulseState heredara de otro estado, se introduciría un acoplamiento innecesario y se podrían heredar comportamientos no deseados.
Al heredar directamente de State, se garantiza que el nuevo estado sea independiente, fácil de entender y de mantener, lo cual es consistente con el objetivo del patrón State.

<img width="1894" height="1098" alt="image" src="https://github.com/user-attachments/assets/b412bfd9-a2eb-4b96-a28e-ca85edeff5db" />

<img width="1860" height="1046" alt="Captura de pantalla 2026-04-16 230916" src="https://github.com/user-attachments/assets/931cf4d3-ad18-4717-a9db-17d43414a104" />

Vemos que al presionar "p" nuestra nueva particula cambia de color, velocidad y pasa cambiando de tamaño entre mas grande y pequeño






