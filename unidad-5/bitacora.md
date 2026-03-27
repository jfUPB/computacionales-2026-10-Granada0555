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

<img width="1192" height="608" alt="image" src="https://github.com/user-attachments/assets/8589c8ec-ab4d-4a30-8022-6f96ed940daf" />

Primero se probó el código de la clase AccessControl, que tiene variables private, protected y public. Al ejecutar el programa con solo la línea ac.publicVar = 10, no ocurrió nada visible en consola. Esto es normal, ya que el programa no tiene ningún cout o impresión, simplemente se ejecuta y termina sin mostrar resultados. Sin embargo, al descomentar las líneas:

ac.protectedVar = 20;
ac.privateVar = 30;

el programa ya no compila. El compilador muestra errores indicando que no se puede acceder a esos miembros. Esto sucede porque protected y private restringen el acceso desde fuera de la clase. En el caso de protected, solo se puede acceder desde clases derivadas, y en el caso de private, únicamente desde la misma clase. De esto se concluye que los modificadores de acceso en C++ sí controlan quién puede acceder a los datos, pero lo hacen en tiempo de compilación, evitando que el código incorrecto siquiera se ejecute.

<img width="1469" height="253" alt="image" src="https://github.com/user-attachments/assets/af02ee0c-f0b0-46f4-9a28-1c5b4b7db98e" />

Luego se probó el segundo programa con la clase MyClass. Al intentar acceder directamente a obj.secret1, el compilador también genera un error, ya que ese atributo es privado. Esto confirma nuevamente que el encapsulamiento impide el acceso directo desde fuera de la clase mientras se está compilando el programa.

<img width="1227" height="635" alt="image" src="https://github.com/user-attachments/assets/b780e8e1-ce56-4e75-b375-ec7e65d7b347" />

Después se utilizó el tercer código, donde se emplea reinterpret_cast para acceder directamente a la memoria del objeto. En este caso, el programa sí compila y se ejecuta correctamente, mostrando los valores de secret1, secret2 y secret3, a pesar de que son privados.
Esto ocurre porque en tiempo de ejecución la memoria no “recuerda” los modificadores de acceso. El objeto simplemente es un bloque de memoria contigua, y al usar punteros se puede acceder directamente a esos valores, ignorando completamente el encapsulamiento. A partir de esto se puede concluir que el encapsulamiento en C++ no es una protección absoluta en tiempo de ejecución, sino una regla que el compilador hace cumplir durante la compilación. Es decir, sirve para organizar y proteger el código a nivel de diseño, pero no impide que alguien con conocimiento técnico acceda a la memoria directamente.

En pocas palabras, el encapsulamiento es una forma de controlar el acceso a los datos de una clase, definiendo qué se puede usar desde afuera y qué no. Es importante porque ayuda a evitar errores, protege la integridad de los datos y hace que el código sea más ordenado y mantenible.

ACTIVIDAD 5 -----------------------------

(Utilizando los codigos de la actividad 2 de referencia )

<img width="947" height="163" alt="image" src="https://github.com/user-attachments/assets/39a24cc6-dea0-478a-8bad-a4237077a0a4" />

Al analizar un objeto de tipo CircularExplosion en el depurador, se puede observar cómo la memoria refleja directamente la jerarquía de herencia. En este caso, CircularExplosion hereda de ExplosionParticle, y esta a su vez hereda de Particle, ademas cuando, se inspecciona el objeto en memoria, se nota que no está dividido en partes separadas, sino que todo se encuentra en un solo bloque continuo. Primero aparecen los elementos correspondientes a la clase base Particle, luego los de ExplosionParticle y finalmente los de CircularExplosion. Esto indica que C++ organiza los objetos heredados colocando primero la base y luego las clases derivadas dentro del mismo espacio de memoria, aunque la clase Particle no tiene atributos propios, sí contiene métodos virtuales, por lo que el objeto incluye un puntero interno llamado _vptr, que apunta a la tabla de funciones virtuales (_vtable). Por otro lado, los atributos reales que ocupan espacio en memoria provienen principalmente de ExplosionParticle, como la posición, la velocidad, el color, la edad, el tiempo de vida y el tamaño. A partir de esto, se puede concluir que la herencia en C++ se implementa de forma secuencial en memoria, lo que permite que un puntero de tipo Particle* pueda apuntar a cualquier objeto derivado sin problemas, ya que la parte base siempre está al inicio del objeto.

<img width="1880" height="788" alt="image" src="https://github.com/user-attachments/assets/92aed57d-debf-4327-ba4e-368ad021bcc7" />

Al analizar un objeto de tipo CircularExplosion en el depurador, se puede observar cómo la memoria refleja directamente la jerarquía de herencia. En este caso, CircularExplosion hereda de ExplosionParticle, y esta a su vez hereda de Particle. Cuando se inspecciona el objeto en memoria, se nota que no está dividido en partes separadas, sino que todo se encuentra en un solo bloque continuo. Primero aparecen los elementos correspondientes a la clase base Particle, luego los de ExplosionParticle y finalmente los de CircularExplosion. Esto indica que C++ organiza los objetos heredados colocando primero la base y luego las clases derivadas dentro del mismo espacio de memoria.

Aunque la clase Particle no tiene atributos propios, sí contiene métodos virtuales, por lo que el objeto incluye un puntero interno llamado _vptr, que apunta a la tabla de funciones virtuales (_vtable). Por otro lado, los atributos reales que ocupan espacio en memoria provienen principalmente de ExplosionParticle, como la posición, la velocidad, el color, la edad, el tiempo de vida y el tamaño. A partir de esto, se puede concluir que la herencia en C++ se implementa de forma secuencial en memoria, lo que permite que un puntero de tipo Particle* pueda apuntar a cualquier objeto derivado sin problemas, ya que la parte base siempre está al inicio del objeto.


<img width="1883" height="941" alt="image" src="https://github.com/user-attachments/assets/14650369-9c2e-4c81-bf72-7fa9beae106c" />

Este comportamiento corresponde al polimorfismo en tiempo de ejecución. Internamente, esto funciona gracias a los métodos virtuales y a la tabla de funciones virtuales. Cada objeto contiene un puntero a su _vtable, que almacena las direcciones de las funciones correspondientes a su tipo real. Cuando se llama a update() a través de un puntero Particle*, el programa consulta esa tabla y ejecuta la versión correcta del método según el tipo del objeto. Esto significa que, aunque el código sea el mismo, el comportamiento cambia dependiendo del objeto que se esté utilizando. En otras palabras, el polimorfismo permite tratar diferentes tipos de objetos como si fueran uno solo, manteniendo comportamientos distintos.


ACTIVIDAD 6  ----------------------------


ofApp.h //////////////////////////////////////////////////////////////
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------- Clase base --------------------
class Particle {
public:
    virtual ~Particle() {}
    virtual void update(float dt) = 0;
    virtual void draw() = 0;
    virtual bool isDead() const = 0;
    virtual bool shouldExplode() const { return false; }
    virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
    virtual ofColor getColor() const { return ofColor(255); }
};

// -------------------- RisingParticle --------------------
class RisingParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float lifetime;
    float age;
    bool exploded;

public:
    RisingParticle(const glm::vec2& pos, const glm::vec2& vel,
                   const ofColor& col, float life)
        : position(pos), velocity(vel), color(col),
          lifetime(life), age(0), exploded(false) {}

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        velocity.y += 9.8f * dt * 8;

        float explosionThreshold = ofGetHeight() * 0.15f + ofRandom(-30, 30);
        if (position.y <= explosionThreshold || age >= lifetime) {
            exploded = true;
        }
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, 10);
    }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// -------------------- NUEVA 1: ZigZagParticle --------------------
class ZigZagParticle : public RisingParticle {
public:
    ZigZagParticle(const glm::vec2& pos, const glm::vec2& vel,
                   const ofColor& col, float life)
        : RisingParticle(pos, vel, col, life) {}

    void update(float dt) override {
        position += velocity * dt;
        age += dt;

        // Movimiento en zigzag
        position.x += sin(age * 10) * 5;

        velocity.y += 9.8f * dt * 8;

        if (age >= lifetime) {
            exploded = true;
        }
    }

    void draw() override {
        ofSetColor(color);
        ofDrawRectangle(position.x, position.y, 8, 8);
    }
};

// -------------------- NUEVA 2: SpiralParticle --------------------
class SpiralParticle : public RisingParticle {
public:
    SpiralParticle(const glm::vec2& pos, const glm::vec2& vel,
                   const ofColor& col, float life)
        : RisingParticle(pos, vel, col, life) {}

    void update(float dt) override {
        age += dt;

        float angle = age * 5;
        position.x += cos(angle) * 4;
        position.y += velocity.y * dt;

        if (age >= lifetime) {
            exploded = true;
        }
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, 6);
    }
};

// -------------------- Explosion base --------------------
class ExplosionParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float age;
    float lifetime;
    float size;

public:
    ExplosionParticle(const glm::vec2& pos, const glm::vec2& vel,
                      const ofColor& col, float life, float sz)
        : position(pos), velocity(vel), color(col),
          age(0), lifetime(life), size(sz) {}

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        float alpha = ofMap(age, 0, lifetime, 255, 0, true);
        color.a = alpha;
    }

    bool isDead() const override { return age >= lifetime; }
};

// -------------------- Tipos existentes --------------------
class CircularExplosion : public ExplosionParticle {
public:
    CircularExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(80, 200);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, size);
    }
};

class RandomExplosion : public ExplosionParticle {
public:
    RandomExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
        velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
    }

    void draw() override {
        ofSetColor(color);
        ofDrawRectangle(position.x, position.y, size, size);
    }
};

class StarExplosion : public ExplosionParticle {
public:
    StarExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(90, 180);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, size);
    }
};

// -------------------- NUEVA EXPLOSIÓN --------------------
class ChaosExplosion : public ExplosionParticle {
public:
    ChaosExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(10, 30)) {
        velocity = glm::vec2(ofRandom(-300, 300), ofRandom(-300, 300));
    }

    void draw() override {
        ofSetColor(color);

        int shape = (int)ofRandom(3);
        if (shape == 0) {
            ofDrawCircle(position, size);
        } else if (shape == 1) {
            ofDrawRectangle(position.x, position.y, size, size);
        } else {
            ofDrawTriangle(position,
                           position + glm::vec2(size, 0),
                           position + glm::vec2(0, size));
        }
    }
};

// -------------------- ofApp --------------------
class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();
    void mousePressed(int x, int y, int button);
    void keyPressed(int key);

    std::vector<Particle*> particles;
    ~ofApp();

private:
    void createRisingParticle();
};
////////////////////////////////////////////////////////////

ofApp.cpp     /////////////////////////////////////////////////

#include "ofApp.h"

void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
}

void ofApp::update() {
    float dt = ofGetLastFrameTime();

    for (int i = 0; i < particles.size(); i++) {
        particles[i]->update(dt);
    }

    for (int i = particles.size() - 1; i >= 0; i--) {

        if (particles[i]->shouldExplode()) {

            int explosionType = (int)ofRandom(4);
            int numParticles = (int)ofRandom(30, 60);

            for (int j = 0; j < numParticles; j++) {

                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(
                        particles[i]->getPosition(), particles[i]->getColor()));

                } else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(
                        particles[i]->getPosition(), particles[i]->getColor()));

                } else if (explosionType == 2) {
                    particles.push_back(new StarExplosion(
                        particles[i]->getPosition(), particles[i]->getColor()));

                } else {
                    particles.push_back(new ChaosExplosion(
                        particles[i]->getPosition(), particles[i]->getColor()));
                }
            }

            delete particles[i];
            particles.erase(particles.begin() + i);

        } else if (particles[i]->isDead()) {
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
    }
}

void ofApp::draw() {
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->draw();
    }
}

void ofApp::createRisingParticle() {

    float minX = ofGetWidth() * 0.35f;
    float maxX = ofGetWidth() * 0.65f;

    glm::vec2 pos(ofRandom(minX, maxX), ofGetHeight());

    glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300),
                     ofGetHeight() * 0.1f);

    glm::vec2 dir = glm::normalize(target - pos);
    glm::vec2 vel = dir * ofRandom(250, 350);

    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);

    float life = ofRandom(1.5f, 3.5f);

    int type = (int)ofRandom(3);

    if (type == 0) {
        particles.push_back(new RisingParticle(pos, vel, col, life));
    } else if (type == 1) {
        particles.push_back(new ZigZagParticle(pos, vel, col, life));
    } else {
        particles.push_back(new SpiralParticle(pos, vel, col, life));
    }
}

void ofApp::mousePressed(int x, int y, int button) {
    createRisingParticle();
}

void ofApp::keyPressed(int key) {
    if (key == ' ') {
        for (int i = 0; i < 300; i++) {
            createRisingParticle();
        }
    }
}

ofApp::~ofApp() {
    for (int i = 0; i < particles.size(); i++) {
        delete particles[i];
    }
    particles.clear();
}

///////////////////////////////////////////////////////////////////////////

El programa está organizado usando programación orientada a objetos. Existe una clase base llamada Particle, de la cual se derivan otros tipos de partículas.


<img width="1836" height="854" alt="image" src="https://github.com/user-attachments/assets/fc8173d2-06d6-4c7f-962e-3fbeb9f655ce" />

<img width="974" height="736" alt="image" src="https://github.com/user-attachments/assets/4fa73754-b85a-4b2e-b834-106ac835717e" />


Por un lado está RisingParticle, que representa las partículas que suben desde la parte inferior de la pantalla y luego explotan. Por otro lado está ExplosionParticle, que sirve como base para las partículas que aparecen después de la explosión. A partir de estas clases base se crean distintos comportamientos usando herencia.

En cuanto a las modificaciones realizadas, se agregaron dos nuevos tipos de partículas:
 - ZigZagParticle, que se mueve en forma de zigzag modificando su posición en el eje X usando una función seno.
 - SpiralParticle, que tiene un movimiento más circular, simulando una especie de espiral.

También se agregó un nuevo tipo de explosión llamado ChaosExplosion, que genera partículas con direcciones completamente aleatorias y además dibuja distintas formas como círculos, rectángulos y triángulos. Adicionalmente, se hizo que el sistema fuera más aleatorio en general. Ahora el tipo de partícula que se crea, el tipo de explosión, la cantidad de partículas generadas y hasta las formas que se dibujan cambian de manera aleatoria. Esto hace que la simulación sea más variada sin modificar demasiado la estructura original del programa.


<img width="1906" height="734" alt="image" src="https://github.com/user-attachments/assets/f670773d-bbb2-4a28-8e69-82d0d32215c4" />


Al inspeccionar una partícula como ZigZagParticle en el depurador, se puede ver cómo están organizados los datos en memoria. Primero aparecen los atributos de la clase base Particle, luego los de RisingParticle y finalmente los propios de ZigZagParticle.Esto muestra que en C++ la herencia se implementa organizando los datos de forma secuencial, donde la subclase contiene internamente a sus clases base.


<img width="1885" height="877" alt="image" src="https://github.com/user-attachments/assets/aa3daa72-c5b4-42b8-9234-a1e103ea0ca8" />

Las clases que tienen métodos virtuales utilizan una tabla llamada _vtable. Esta tabla guarda referencias a las funciones que cada objeto debe ejecutar.
Al comparar dos clases como CircularExplosion y ChaosExplosion, se observa que ambas comparten algunas funciones heredadas, pero tienen implementaciones distintas en métodos como draw(). Esto demuestra que cada clase tiene su propia _vtable, y que esta cambia dependiendo de las funciones que la clase sobrescribe.

<img width="1850" height="848" alt="image" src="https://github.com/user-attachments/assets/142d5c6e-9027-4c71-bc6f-3b38f923a83e" />

En el método update() del programa se recorre un vector de Particle* y se llama a update(dt) sin importar el tipo real de cada objeto, aun así, cada partícula ejecuta su propio comportamiento. Por ejemplo, ZigZagParticle se mueve en zigzag y SpiralParticle se mueve en forma circular. Esto ocurre porque el programa decide qué función ejecutar en tiempo de ejecución, lo cual es el polimorfismo.

<img width="1300" height="204" alt="image" src="https://github.com/user-attachments/assets/feff2eb9-9066-4f47-8e7e-80ba7e276837" />

En las clases se usan atributos protegidos (protected), lo que permite que las subclases accedan a ellos. Por ejemplo, variables como position o velocity pueden ser utilizadas directamente en las clases hijas, ademas si estas variables fueran privadas (private), no podrían ser accedidas desde las subclases. En el depurador también se puede observar qué atributos pertenecen a cada clase, lo que ayuda a entender cómo se organiza el acceso a los datos.




https://github.com/user-attachments/assets/e75866bb-5c84-4fde-8edd-04ac4c355e80


El ciclo de vida de una partícula es claro: Primero se crea y se agrega al vector. Luego se actualiza en cada frame usando el método update(). Cuando cumple ciertas condiciones, como el tiempo de vida o la altura, la partícula explota. Finalmente, se elimina del vector y se libera la memoria usando delete. Esto muestra que el objeto pasa por todas sus etapas correctamente. (Anexare un video para que se vea mucho mejor)
