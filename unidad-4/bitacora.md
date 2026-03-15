Actividad 1 - Unidad 4


<img width="1919" height="1138" alt="Captura de pantalla 2026-03-06 152020" src="https://github.com/user-attachments/assets/6d2f478e-6f51-4afc-8df3-23b1148aeb14" />

Al ejecutar el programa aparece en la pantalla una escena llena de colores en movimiento y una especie de figura que se comporta como una serpiente que sigue el cursor del mouse. Esta serpiente está formada por muchos puntos conectados entre sí que se mueven de manera suave, dando la sensación de que todo fluye. Detrás de este efecto visual hay una estructura de datos llamada lista enlazada, que se utiliza para guardar la posición de cada uno de esos puntos. Gracias a esta lista, el programa puede manejar fácilmente todos los segmentos de la serpiente y hacer que se muevan juntos.

<img width="1919" height="1111" alt="Captura de pantalla 2026-03-06 152004" src="https://github.com/user-attachments/assets/3e0ebf0a-a096-4356-ac4d-aff8ba2b3a9b" />

Cuando el programa comienza, la función setup() se encarga de preparar todo para que la animación funcione. Primero se define el color inicial del fondo y luego se crean varios puntos que formarán la serpiente. Todos esos puntos se colocan al principio en el centro de la pantalla, por lo que al inicio parece que están todos superpuestos. Se crean alrededor de veinte puntos, y cada uno se guarda dentro de la lista. Estos puntos serán los que después se moverán para formar la serpiente que se ve en pantalla.

<img width="1919" height="1144" alt="Captura de pantalla 2026-03-06 151952" src="https://github.com/user-attachments/assets/6479e424-887b-44a7-b963-f6ee29d98973" />
<img width="1918" height="1139" alt="Captura de pantalla 2026-03-06 151943" src="https://github.com/user-attachments/assets/b60f9c84-22ab-46dc-a58c-bf997179fbf6" />
<img width="1919" height="1140" alt="Captura de pantalla 2026-03-06 152030" src="https://github.com/user-attachments/assets/286a970c-9e83-4499-a51d-279ba7a10e26" />

Después entra en funcionamiento la parte más importante, que es la función update(). Aquí el programa toma la posición actual del mouse y la usa como objetivo. El primer punto de la serpiente se mueve poco a poco hacia el cursor, y luego cada punto siguiente se mueve hacia el punto que tiene delante. Esto hace que todos los segmentos se sigan entre sí y que el movimiento se vea natural, como si fuera una serpiente real desplazándose. Al mismo tiempo, el programa también va cambiando poco a poco el color del fondo, lo que produce ese efecto de gradiente que cambia constantemente.

Luego, en la función draw(), todo lo que se calculó se dibuja en la pantalla. Primero aparece un fondo con un degradado de colores que cambia con el tiempo. Después se dibuja una línea que conecta todos los puntos de la serpiente, formando una curva suave. Finalmente se dibujan círculos en cada punto. Estos círculos cambian de tamaño y de color dependiendo de su posición en la serpiente, lo que hace que el efecto visual sea más interesante y que la figura resalte sobre el fondo.

Además, el programa permite interactuar usando algunas teclas. Si se presiona “c”, todos los puntos de la serpiente se eliminan y la figura desaparece. Si se presiona “a”, se agrega un nuevo punto en una posición aleatoria de la pantalla, haciendo que la serpiente crezca. Con la tecla “r” se elimina el último punto, reduciendo su tamaño. Y si se presiona “s”, el programa guarda una captura de pantalla del momento actual. Estas acciones permiten experimentar con la serpiente y ver cómo cambia su forma mientras se mueve por la pantalla.

<img width="1917" height="1141" alt="Captura de pantalla 2026-03-04 171211" src="https://github.com/user-attachments/assets/22dc9e89-1cce-4fd5-8bc6-499bc3b8ab6b" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------
Actividad 2


El programa analizado fue desarrollado en C++ utilizando el framework openFrameworks, el cual es una herramienta ampliamente usada para programación creativa y visualizaciones interactivas. Este framework permite trabajar con gráficos en tiempo real, interacción con el usuario y animaciones de manera relativamente sencilla en comparación con trabajar directamente con librerías gráficas más complejas. En este caso, el programa crea una animación que simula una especie de serpiente formada por varios nodos que siguen el movimiento del mouse en la pantalla. El comportamiento visual del programa depende principalmente de una estructura de datos tipo lista enlazada, la cual permite almacenar y recorrer dinámicamente cada segmento de la serpiente. Durante el análisis del código se utilizó el depurador del entorno de desarrollo para observar cómo se comportaban las variables y cómo se recorría la estructura en memoria, lo cual permitió entender mejor el funcionamiento del algoritmo.

Para representar cada segmento de la serpiente se utiliza una clase llamada Node. Esta clase contiene principalmente dos atributos: la posición del nodo en pantalla y un puntero al siguiente nodo de la lista. La posición se almacena usando glm::vec2, que es un tipo de dato utilizado por la librería matemática asociada a OpenGL llamada OpenGL Mathematics. Este tipo de dato permite guardar coordenadas bidimensionales, es decir, valores de posición en los ejes X y Y. El segundo atributo es un puntero llamado next, el cual apunta al siguiente nodo dentro de la lista. Gracias a este puntero es posible conectar un nodo con otro y formar una cadena de nodos. Cuando se crea un nodo nuevo mediante el constructor de la clase, este se inicializa con una posición específica y el puntero next se establece en nullptr, lo que indica que inicialmente no está conectado a ningún otro nodo.

<img width="1664" height="956" alt="Captura de pantalla 2026-03-11 145942" src="https://github.com/user-attachments/assets/2606d19f-92ca-491b-af1e-c0722049ac3e" />

La administración de los nodos se realiza mediante la clase LinkedList, que implementa una lista enlazada simple. Esta clase contiene tres variables principales: head, que apunta al primer nodo de la lista; tail, que apunta al último nodo; y size, que guarda la cantidad total de nodos presentes en la lista. Esta estructura permite agregar o eliminar nodos dinámicamente mientras el programa está en ejecución. Por ejemplo, la función push_back permite agregar un nuevo nodo al final de la lista. El proceso consiste en crear un nodo dinámicamente utilizando la palabra reservada new y luego conectarlo al último nodo existente. Si la lista está vacía, el nuevo nodo se convierte tanto en el head como en el tail. Si la lista ya contiene nodos, el nodo actual al final de la lista apunta al nuevo nodo mediante su puntero next, y luego el tail se actualiza para apuntar al nodo recién creado. Este mecanismo permite que la serpiente pueda crecer agregando nuevos segmentos.

Otra función importante es pop_back, la cual se encarga de eliminar el último nodo de la lista. Si la lista está vacía, la función simplemente termina sin realizar ninguna acción. Si solo existe un nodo, este se elimina y los punteros head y tail se establecen en nullptr. Sin embargo, si existen varios nodos, el algoritmo debe recorrer la lista desde el inicio hasta encontrar el penúltimo nodo. Una vez localizado, se elimina el último nodo usando delete, y el penúltimo nodo se convierte en el nuevo tail. Este proceso demuestra cómo las listas enlazadas requieren recorrer los nodos para encontrar ciertas posiciones, ya que no existe acceso directo por índice como en los arreglos. También existe una función llamada clear, la cual recorre toda la lista eliminando cada nodo de forma segura para liberar la memoria utilizada y evitar fugas de memoria.

En la función setup del programa se realiza la inicialización de la serpiente. En esta parte se ejecuta un ciclo que crea veinte nodos utilizando la función push_back. Todos estos nodos se inicializan en la posición central de la pantalla utilizando las funciones ofGetWidth() y ofGetHeight(), que obtienen el ancho y alto de la ventana. Esto significa que al iniciar el programa la serpiente aparece como una serie de nodos superpuestos en el centro de la pantalla. A partir de ese momento, el comportamiento dinámico de la serpiente se controla dentro de la función update, la cual se ejecuta continuamente mientras el programa está activo.

La parte más importante del análisis se encuentra en el bloque de código donde se recorre la lista de nodos. Primero se crea un puntero llamado current que apunta al primer nodo de la lista, es decir, snake.head. Luego se utiliza un ciclo while que se ejecuta mientras current no sea nullptr. Esto significa que el ciclo continuará hasta llegar al final de la lista. Dentro de este ciclo ocurre la lógica principal que permite que los nodos se muevan de forma suave. La posición de cada nodo se actualiza utilizando la función glm::mix, la cual realiza una interpolación lineal entre dos valores. Matemáticamente, esta función calcula un valor intermedio entre una posición inicial y una posición objetivo utilizando un factor de interpolación. En este caso, el factor utilizado es 0.2, lo que significa que cada nodo se mueve aproximadamente un veinte por ciento hacia el objetivo en cada actualización del programa. Esto genera un movimiento progresivo en lugar de un movimiento brusco.


<img width="1622" height="923" alt="Captura de pantalla 2026-03-11 145935" src="https://github.com/user-attachments/assets/08402616-4116-4106-8c66-9d02ff2682fd" />
<img width="1524" height="987" alt="Captura de pantalla 2026-03-11 145930" src="https://github.com/user-attachments/assets/bcbecf30-7240-4a2a-9685-7700beec9ade" />

Algo interesante del algoritmo es que el objetivo inicial corresponde a la posición del mouse en la pantalla. Sin embargo, después de actualizar la posición del primer nodo, la variable target se actualiza con la posición de ese mismo nodo. Esto provoca que el segundo nodo ya no siga directamente al mouse, sino al nodo anterior. El mismo proceso se repite con todos los nodos de la lista, generando una cadena de movimiento donde cada segmento sigue al que está delante de él. Este comportamiento es lo que produce el efecto visual de una serpiente o cola que se mueve de forma fluida siguiendo el cursor del usuario.

Durante el proceso de depuración se utilizó el depurador para observar el comportamiento de las variables dentro del ciclo. En las capturas de pantalla se puede ver cómo el puntero current inicialmente apunta al primer nodo de la lista. A medida que el ciclo se ejecuta, el puntero se va actualizando con current = current->next, lo que permite avanzar al siguiente nodo. También se pueden observar los cambios en la variable target, la cual se actualiza constantemente con la posición del nodo actual. Estas observaciones son importantes porque demuestran que el algoritmo realmente está recorriendo toda la lista enlazada y que cada nodo está actualizando su posición correctamente.

<img width="1681" height="1044" alt="Captura de pantalla 2026-03-11 150049" src="https://github.com/user-attachments/assets/c28d8dde-3557-47f2-b142-910901fbd662" />
<img width="1897" height="1049" alt="Captura de pantalla 2026-03-11 150029" src="https://github.com/user-attachments/assets/3093402d-ac0d-493e-9cb1-6ebbdf9244e1" />

Finalmente, en la función draw se realiza la representación visual de la serpiente. Para esto se utiliza un objeto ofMesh, que permite dibujar líneas conectando los nodos en orden. Además, cada nodo se dibuja también como un círculo cuyo tamaño disminuye gradualmente a lo largo de la serpiente. Los colores se generan utilizando el modelo HSB, lo que permite crear un degradado de colores que cambia dinámicamente con el tiempo. Este efecto visual se complementa con un fondo de colores que también cambia gradualmente, generando una animación más dinámica y atractiva visualmente.

-------------------------------------------------------------------------------------------------------------------------------------------------------------

Actividad 3

En esta actividad se desarrolló un programa en C++ usando el framework openFrameworks con el objetivo de implementar desde cero una estructura de datos tipo cola FIFO (First In, First Out). La idea principal del programa es generar un efecto visual de pintura dinámica en la pantalla. Cada vez que el usuario mueve o mantiene presionado el mouse, el programa crea un nuevo trazo que se dibuja en la ventana. No obstante, para evitar que se acumulen demasiados trazos y que el programa consuma más memoria de la necesaria, se utiliza una cola que limita la cantidad de elementos almacenados. Esto significa que cuando se alcanza el tamaño máximo permitido, el trazo más antiguo se elimina automáticamente para dejar espacio a uno nuevo. De esta manera, el programa puede seguir agregando trazos recientes mientras los más viejos desaparecen gradualmente, manteniendo un número controlado de elementos visibles en pantalla.

En OfApp.h:
#pragma once
#include "ofMain.h"

//* Nodo de la cola
struct Node {

    float x;
    float y;
    float radius;
    ofColor color;
    float opacity;

    Node* next;

};

// Cola FIFO
class BrushQueue {

public:

    Node* front;
    Node* rear;

    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);

    void dequeue();

    void clear();

    bool isEmpty();

};


// Constructor simple
BrushQueue::BrushQueue(int _maxSize)
{
    front = nullptr;
    rear = nullptr;
    size = 0;
    maxSize = _maxSize;
}


// Destructor
BrushQueue::~BrushQueue()
{
    clear();
}


// Agregar nodo al final de la cola
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity)
{

    Node* newNode = new Node;

    newNode->x = x;
    newNode->y = y;
    newNode->radius = radius;
    newNode->color = color;
    newNode->opacity = opacity;

    newNode->next = nullptr;

    if (front == nullptr)
    {
        front = newNode;
        rear = newNode;
    }
    else
    {
        rear->next = newNode;
        rear = newNode;
    }

    size = size + 1;

    if (size > maxSize)
    {
        dequeue();
    }

}


// Eliminar el nodo más antiguo
void BrushQueue::dequeue()
{

    if (front == nullptr)
    {
        return;
    }

    Node* temp;

    temp = front;

    front = front->next;

    delete temp;

    size = size - 1;

    if (front == nullptr)
    {
        rear = nullptr;
    }

}


// Eliminar todos los nodos
void BrushQueue::clear()
{

    while (front != nullptr)
    {

        Node* temp;

        temp = front;

        front = front->next;

        delete temp;

    }

    rear = nullptr;

    size = 0;

}


// Verificar si está vacía
bool BrushQueue::isEmpty()
{

    if (front == nullptr)
    {
        return true;
    }

    return false;

}



class ofApp : public ofBaseApp {

public:

    BrushQueue strokes;

    float backgroundHue;

    ofApp() : strokes(50)
    {
        backgroundHue = 0;
    }

    void setup();
    void update();
    void draw();
    void keyPressed(int key);

};
*//

---------------------------------------------------------------------------------------------------------

//*
En ofApp.cpp:

#include "ofApp.h"


//--------------------------------------------------------------
void ofApp::setup()
{
    ofBackground(0);
}


//--------------------------------------------------------------
void ofApp::update()
{

    backgroundHue = backgroundHue + 0.2;

    if (backgroundHue > 255)
    {
        backgroundHue = 0;
    }


    if (ofGetMousePressed())
    {

        float x = ofGetMouseX();
        float y = ofGetMouseY();

        float radius = ofRandom(5, 25);

        ofColor color;

        color.setHsb(ofRandom(255), 200, 255);

        float opacity = 200;

        strokes.enqueue(x, y, radius, color, opacity);

    }

}


//--------------------------------------------------------------
void ofApp::draw()
{

    ofColor color1;
    ofColor color2;

    color1.setHsb(backgroundHue, 150, 240);

    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);

    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);


    Node* current;

    current = strokes.front;

    int index = 0;

    while (current != nullptr)
    {

        float fade;

        fade = ofMap(index, 0, strokes.size, 255, 50);

        ofSetColor(current->color, fade);

        ofDrawCircle(current->x, current->y, current->radius);

        current = current->next;

        index = index + 1;

    }

}


//--------------------------------------------------------------
void ofApp::keyPressed(int key)
{

    if (key == 'c')
    {
        strokes.clear();
    }

    if (key == 'a')
    {

        if (strokes.maxSize == 50)
        {
            strokes.maxSize = 100;
        }
        else
        {
            strokes.maxSize = 50;
        }

    }

    else if (key == 's')
    {
        ofSaveFrame();
    }

}

*//

<img width="1879" height="1052" alt="image" src="https://github.com/user-attachments/assets/f149b929-f594-4d8e-b24c-6a15d640e7c1" />
<img width="1919" height="1126" alt="image" src="https://github.com/user-attachments/assets/f4e147c5-e828-4a7c-86d9-e0f2c8b91fe7" />
<img width="1916" height="1065" alt="image" src="https://github.com/user-attachments/assets/8f81c822-dfa1-4b71-bd5c-303c5ca4e489" />
<img width="1919" height="1108" alt="image" src="https://github.com/user-attachments/assets/c61667d8-c331-4f38-a069-525a0a026598" />
Para implementar esta estructura de datos se creó una estructura llamada Node, que representa cada trazo de pintura almacenado en la cola. Cada nodo contiene la información necesaria para dibujar un trazo en la pantalla: la posición en los ejes X y Y, el radio del círculo que representa el trazo, el color del trazo y su nivel de opacidad. Además, cada nodo contiene un puntero llamado next, que apunta al siguiente nodo dentro de la cola. Este puntero permite enlazar los nodos entre sí formando una lista enlazada simple. El uso de punteros es fundamental en este tipo de estructuras porque permite crear estructuras dinámicas que pueden crecer o disminuir durante la ejecución del programa sin necesidad de definir un tamaño fijo desde el inicio.

La estructura de datos principal del programa es la clase BrushQueue, que implementa manualmente una cola utilizando nodos enlazados. Esta clase contiene dos punteros principales llamados front y rear. El puntero front apunta al primer elemento de la cola, es decir, el nodo más antiguo, mientras que el puntero rear apunta al último elemento, que corresponde al nodo más reciente que ha sido agregado. Además de estos punteros, la cola mantiene dos variables enteras llamadas size y maxSize. La variable size permite llevar un control del número actual de nodos almacenados, mientras que maxSize define el tamaño máximo que la cola puede alcanzar antes de que se deban eliminar elementos antiguos. Esta información es necesaria para controlar el comportamiento de la cola y garantizar que se respete la lógica FIFO.

La función enqueue se encarga de agregar nuevos nodos al final de la cola. Cuando se ejecuta esta función, primero se crea un nuevo nodo utilizando memoria dinámica con la palabra reservada new. Luego se asignan los valores correspondientes a la posición, el radio, el color y la opacidad del trazo. Después de inicializar el nodo, se verifica si la cola está vacía. Si front es nullptr, significa que no hay elementos en la cola y por lo tanto el nuevo nodo se convierte tanto en el primer como en el último elemento. En cambio, si la cola ya contiene nodos, el nodo actual que está al final apunta al nuevo nodo mediante su puntero next, y posteriormente el puntero rear se actualiza para que apunte al nodo recién creado. Finalmente se incrementa la variable size. Si después de agregar el nodo el tamaño de la cola supera el límite establecido por maxSize, se ejecuta automáticamente la función dequeue para eliminar el elemento más antiguo.

<img width="1919" height="1109" alt="image" src="https://github.com/user-attachments/assets/b6f39218-8c0c-4249-8c98-4bbe33e7346a" />
<img width="1919" height="1048" alt="image" src="https://github.com/user-attachments/assets/9c893205-fa8f-4378-b866-4d973c35f021" />
<img width="1919" height="1073" alt="image" src="https://github.com/user-attachments/assets/a538c6ee-81c1-4982-a147-9ae34a049ed1" />

La función dequeue es la encargada de eliminar el primer nodo de la cola, es decir, el nodo más antiguo. Este comportamiento es lo que define la lógica FIFO, donde el primer elemento que entra es también el primero en salir. El algoritmo primero verifica si la cola está vacía comprobando si front es nullptr. Si la cola contiene nodos, se crea un puntero temporal que apunta al nodo que se va a eliminar. Luego el puntero front se actualiza para que apunte al siguiente nodo de la cola. Después de esto se libera la memoria del nodo antiguo utilizando delete, lo cual es importante para evitar fugas de memoria. Finalmente se decrementa el valor de size. Si después de eliminar el nodo la cola queda vacía, el puntero rear también se establece en nullptr.

Otra función importante dentro de la implementación es clear, la cual se encarga de eliminar completamente todos los nodos de la cola. Esta función utiliza un ciclo while que recorre todos los nodos desde front hasta que no quedan más elementos. En cada iteración se guarda temporalmente el nodo actual, se avanza el puntero front al siguiente nodo y se elimina el nodo anterior con delete. Este procedimiento garantiza que toda la memoria utilizada por la cola sea liberada correctamente. Al finalizar el proceso se restablecen los punteros front y rear a nullptr y se reinicia el tamaño de la cola a cero. Este tipo de manejo de memoria es fundamental cuando se trabaja con estructuras dinámicas en C++.

Dentro del programa principal, el comportamiento interactivo ocurre principalmente en la función update. En esta función se detecta si el usuario está presionando el botón del mouse. Cuando esto ocurre, el programa obtiene la posición actual del cursor y genera un nuevo trazo con un radio aleatorio y un color generado también de manera aleatoria. Este trazo se envía a la cola mediante la función enqueue, lo que provoca que se agregue un nuevo nodo al final de la estructura. Con el tiempo, a medida que el usuario sigue moviendo el mouse, se van agregando nuevos nodos a la cola y los más antiguos se eliminan automáticamente cuando se supera el tamaño máximo.

El dibujo de los trazos se realiza en la función draw. En esta parte del programa se recorre la cola utilizando un puntero que comienza en strokes.front. Mediante un ciclo while, el programa visita cada nodo hasta llegar al final de la lista. En cada iteración se dibuja un círculo utilizando la posición y el radio almacenados en el nodo. Además, se calcula un valor de opacidad que depende de la posición del nodo dentro de la cola. Esto permite que los trazos más antiguos se dibujen con menor intensidad, mientras que los trazos más recientes aparecen más visibles. Este efecto visual crea la sensación de que los trazos se desvanecen gradualmente con el tiempo.

El programa también incluye interacción mediante el teclado. Cuando el usuario presiona la tecla c, se ejecuta la función clear, lo que elimina todos los trazos almacenados en la cola y limpia la pantalla. Si el usuario presiona la tecla a, el tamaño máximo de la cola cambia entre 50 y 100 elementos, lo que permite aumentar o reducir la cantidad de trazos visibles en la pantalla. Finalmente, si se presiona la tecla s, el programa guarda una captura del frame actual utilizando la función ofSaveFrame. Estas interacciones permiten al usuario controlar el comportamiento de la animación mientras el programa está en ejecución.


<img width="1867" height="1079" alt="Captura de pantalla 2026-03-11 151921" src="https://github.com/user-attachments/assets/8969c6c5-e2e9-4790-8d66-56d281976041" />
<img width="1836" height="1131" alt="Captura de pantalla 2026-03-11 151913" src="https://github.com/user-attachments/assets/62931356-a3f3-4d0f-b33e-389b14747298" />

Durante el proceso de depuración se utilizaron breakpoints para observar el comportamiento de la cola en diferentes situaciones. En la primera evidencia se detuvo la ejecución durante la inserción del primer nodo en una cola vacía, observando cómo los punteros front y rear apuntaban al mismo nodo y cómo la variable size cambiaba de cero a uno. En la segunda evidencia se insertaron múltiples nodos y se verificó que el orden de los elementos se mantenía correctamente, demostrando que los nodos se agregaban siempre al final de la estructura. En la tercera evidencia se analizó la función dequeue, observando cómo el puntero front se movía al siguiente nodo y cómo el nodo anterior era eliminado de la memoria con delete, lo que confirma que no se generan fugas de memoria. En la cuarta evidencia se verificó el control del tamaño máximo de la cola, observando cómo al superar maxSize se ejecutaba automáticamente la eliminación del nodo más antiguo. En la quinta evidencia se analizó el recorrido de la cola durante la función draw, confirmando que el programa puede recorrer todos los nodos sin alterar la estructura original. Finalmente, en la sexta evidencia se ejecutó la función clear, comprobando que todos los nodos eran eliminados y que los punteros de la cola volvían a su estado inicial.
<img width="1482" height="1117" alt="image" src="https://github.com/user-attachments/assets/11f88632-8a98-4015-be4a-8692731d0a74" />

Ahora bien resolviendo los breakpoint y las variables/memoria de interés, estan ubicadas en las lineas:

65 — Inserción del primer nodo en cola vacía (front = newNode;)
En esta parte del código se puede ver cuando se inserta el primer nodo dentro de la cola. Esto pasa cuando front es nullptr, lo que significa que todavía no hay ningun elemento guardado en la estructura. Cuando se ejecuta front = newNode, el nodo que acabamos de crear pasa a ser el primer elemento de la cola. Despues también se asigna ese mismo nodo a rear, porque al ser el unico elemento que existe en ese momento, es al mismo tiempo el primero y el ultimo. En el depurador se puede observar que antes de esta linea tanto front como rear estaban en nullptr, y despues de ejecutarla ambos apuntan al mismo nodo en memoria. Esto demuestra que la cola se inicializa correctamente cuando se inserta el primer elemento, lo cual es importante para que la estructura funcione bien desde el inicio.

68 — Inserción manteniendo el orden FIFO (rear->next = newNode;)
Aquí se puede ver cómo se agregan nuevos nodos cuando la cola ya tiene elementos. En este caso el código entra en el else, porque front ya no es nullptr. Lo que ocurre es que el nodo que estaba al final (rear) ahora apunta al nuevo nodo mediante rear->next = newNode. Despues se actualiza rear para que ahora el ultimo nodo de la cola sea el nuevo que se acaba de crear. Si uno mira esto en el depurador, se puede ver como el nodo anterior empieza a apuntar al nuevo nodo, formando una cadena. Esto demuestra que los elementos siempre se agregan al final de la estructura, manteniendo el orden FIFO, es decir, el primero que entra será el primero que salga. Esto es justamente el comportamiento que se espera de una cola.

74 — Control del tamaño máximo de la cola (if (size > maxSize))
En esta linea el programa verifica si la cantidad de nodos almacenados en la cola superó el tamaño máximo permitido. Primero el tamaño se incrementa con size = size + 1, y luego se revisa si ese valor es mayor que maxSize. Si esto sucede, el programa llama a la función dequeue() para eliminar el nodo más antiguo. En el depurador se puede ver claramente cuando size pasa a ser mayor que maxSize, y en ese momento se ejecuta la eliminación. Esto demuestra que el programa controla correctamente el limite de la cola, evitando que se acumulen demasiados nodos y que el programa consuma mas memoria de la necesaria. En el contexto del programa esto es importante porque los trazos del mouse se generan constantemente y si no existiera este control la estructura crecería sin limite.

92 — Eliminación del nodo más antiguo (delete temp; en dequeue())
Esta linea forma parte de la función dequeue(), que se encarga de eliminar el nodo más antiguo de la cola. Primero el nodo al que apunta front se guarda en una variable temporal llamada temp. Luego front avanza al siguiente nodo con front = front->next. Finalmente el nodo antiguo se elimina de memoria usando delete temp. Cuando se observa esto en el depurador, se puede ver que front deja de apuntar al nodo viejo y ahora apunta al siguiente nodo de la lista. Esto demuestra que el elemento más antiguo se elimina correctamente y que la estructura sigue funcionando sin perder el orden de los nodos. Además, el uso de delete es importante para liberar la memoria que ya no se necesita y evitar fugas de memoria dentro del programa.

112 — Limpieza total de la memoria (delete temp; en clear())
En esta parte se encuentra la función clear(), que se utiliza para eliminar todos los nodos de la cola cuando el usuario lo solicita. Esto se hace mediante un ciclo while que se repite mientras front sea diferente de nullptr. En cada iteración se guarda el nodo actual en temp, luego front avanza al siguiente nodo, y finalmente se elimina el nodo anterior con delete temp. Si uno observa esto paso a paso en el depurador, se puede ver cómo cada nodo se va eliminando uno por uno hasta que ya no queda ninguno. Al final rear queda en nullptr y size vuelve a cero. Esto demuestra que la función limpia completamente la estructura y libera toda la memoria utilizada, lo cual es importante para evitar problemas cuando el programa sigue ejecutandose.

(en ofApp.cpp) — Recorrido de la cola sin destruirla (while (current != nullptr))
En esta parte del programa lo que se hace es recorrer todos los nodos de la cola para dibujar los trazos en la pantalla. Se usa un puntero llamado current que comienza apuntando a strokes.front. Luego, dentro del while, el programa utiliza los datos almacenados en cada nodo (como la posición, el radio o el color) para dibujar los círculos. Despues current avanza al siguiente nodo con current = current->next. Lo importante aquí es que en ningun momento se eliminan nodos ni se modifica la estructura de la cola, simplemente se recorren sus elementos. Si se observa en el depurador, se puede ver cómo current va cambiando de nodo hasta llegar a nullptr. Esto demuestra que es posible recorrer la cola para utilizar sus datos sin destruirla, lo cual es necesario para que los trazos sigan existiendo mientras el programa se esta ejecutando.

No me dejo subir la imagen del pantallazo, entonces lo volvi un link: https://drive.google.com/file/d/1PqQUwfis7bXWBwak1MFLgWlFzMMZN-U0/view?usp=drive_link
------------------------------------------------------------------------------------------------------------------------------------------------------------ 

Actividad Final

Paso lo mismo que en la ultima, no me dejo subir ninguna imagen, entonces le comparto un enlace a una carpeta de drive con todos los diagramas

https://drive.google.com/drive/folders/1dZVFBBEyBTkfTxBPfpI4oQblKZcfrrFx?usp=drive_link






