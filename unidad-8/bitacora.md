
----------------------------------- Actividad 1 ------------------------------------------------------

Parte 1) Cuando ejecuté el programa y di clic en la ventana, lo primero que noté fue que la animación del círculo se congelaba. Yo esperaba que siguiera moviéndose mientras se hacía el cálculo, pero no fue así. La razón es que toda la lógica corre en un solo hilo: cuando el flujo principal entra en heavyComputation(), queda ocupado y no puede seguir dibujando. Esto me permitió entender que un proceso con un solo hilo no puede hacer varias cosas al mismo tiempo; cualquier tarea pesada bloquea la interfaz. (la evidencia visual sería simplemente una ventana congelada, que no aporta nada nuevo ni demuestra claramente el concepto. Lo importante es la explicación del bloqueo, no la imagen estática.)

Parte 2) Después de modificar el código para que heavyComputation() corra en un hilo separado, al dar clic la ventana ya no se congela. El círculo sigue moviéndose, lo cual era lo que esperaba. Sin embargo, el cambio de tamaño del círculo no ocurre de inmediato, sino solo cuando el hilo secundario termina su cálculo y actualiza la variable compartida. Esto me mostró que aunque los hilos permiten mantener la interfaz responsiva, las tareas pesadas siguen tardando en completarse y los resultados se reflejan únicamente al finalizar. Aquí aprendí también la importancia de usar mecanismos de sincronización como lock() y unlock() para evitar conflictos al compartir memoria entre hilos. ( aprendí que los hilos permiten mantener la interfaz responsiva, pero las tareas pesadas siguen tardando en completarse. Además, es necesario usar lock() y unlock() para evitar conflictos al compartir memoria).

Parte 3)

  - Concurrencia es cuando varias tareas parecen avanzar al mismo tiempo, pero en realidad se intercalan en un mismo núcleo. Es como si un solo trabajador hiciera varias tareas alternando entre ellas.

  - Paralelismo es cuando varias tareas avanzan realmente al mismo tiempo en distintos núcleos. Es como tener varios trabajadores haciendo tareas diferentes en paralelo. 

Entender esta diferencia es clave al trabajar con hilos: si mi computador tiene un solo núcleo, los hilos me dan concurrencia, pero no paralelismo real. En cambio, si tiene varios núcleos, puedo aprovecharlos para que las tareas pesadas se ejecuten de verdad en paralelo. Esto me ayuda a diseñar programas que no bloqueen la interfaz y que aprovechen mejor el hardware disponible.

<img width="1577" height="846" alt="image" src="https://github.com/user-attachments/assets/96bf5c6e-9b19-46e2-b027-d2595488319c" />

------------------------------------- Actividad 2 ------------------------------------------

Parte 1) Al revisar el código, noté que el acceso a circleSize está protegido con lock() y unlock(). Esto evita que el hilo principal y el hilo secundario la modifiquen al mismo tiempo. Sincronizar con un mutex asegura seguridad, pero puede afectar el rendimiento porque los hilos deben esperar turno. Es como tener varios trabajadores pero solo uno puede usar la herramienta a la vez.

<img width="797" height="612" alt="image" src="https://github.com/user-attachments/assets/9f5dcb71-6576-424c-b69f-8ea8729b12ab" />

Parte 2) Al ejecutar el programa, en modo seguro (SAFE) el contador llega al valor esperado. En modo inseguro (UNSAFE) el contador queda por debajo.
Reflexión: esto ocurre porque la operación ++counter no es atómica. Varios hilos leen el mismo valor, lo incrementan y lo escriben, pero uno sobrescribe al otro. Así se pierden actualizaciones.

<img width="917" height="605" alt="image" src="https://github.com/user-attachments/assets/7d0e0b8a-2b45-43ca-b4fa-e59386553fbc" />
<img width="399" height="432" alt="image" src="https://github.com/user-attachments/assets/6457562a-4d8b-425a-8b21-afe285669b36" />

Parte 3) La condición de carrera se presenta porque varios hilos intentan modificar counter al mismo tiempo sin coordinación.
Ejemplo humanizado: imagina cuatro personas contando monedas y anotando el total en la misma hoja. Si dos leen “100”, suman una moneda y escriben “101” al mismo tiempo, el resultado final será “101” en vez de “102”. Eso es exactamente lo que pasa con counter en modo inseguro.

<img width="991" height="382" alt="image" src="https://github.com/user-attachments/assets/61213dee-47c5-49f5-88ec-d368c2586a75" />

---------------------------- Actividad 3 --------------------------------

SECUENCIAL

<img width="661" height="587" alt="image" src="https://github.com/user-attachments/assets/02063c1a-4934-478e-9c2f-61176a7dfd33" />

Cuando ejecuté el programa en su versión secuencial y presioné la tecla ESPACIO, lo primero que noté fue que la ventana se congelaba por completo. El fractal tardaba varios segundos en aparecer y durante ese tiempo no podía interactuar con la aplicación. Esto me hizo sentir que el cálculo era demasiado pesado para un solo flujo de instrucciones. Al final, la imagen se generaba correctamente, pero el tiempo de espera era alto y la experiencia poco fluida.

Lo que ocurre es que el algoritmo recorre píxel por píxel en un único hilo, sin aprovechar los múltiples núcleos del procesador. Toda la carga de trabajo se concentra en un solo camino de ejecución, lo que explica la lentitud y el bloqueo de la interfaz. Esta versión me permitió comprender las limitaciones de trabajar de manera secuencial: aunque el resultado es correcto, el rendimiento es pobre y no se aprovecha el hardware moderno.

PARALELA

<img width="506" height="454" alt="image" src="https://github.com/user-attachments/assets/26c61e67-d244-4a57-9a13-1e532227a263" />

Al ejecutar la versión paralela, la experiencia cambió bastante. Al presionar ESPACIO, el cálculo se repartió entre varios hilos y cada uno se encargó de un bloque de filas de la imagen. La ventana ya no se sintió tan bloqueada y el fractal apareció mucho más rápido. El programa incluso mostraba cuántos hilos estaban activos, y pude comprobar que el tiempo de cálculo disminuía de manera notable en comparación con la versión secuencial.

Aquí entendí que el paralelismo no es solo teoría: realmente permite que el hardware trabaje en conjunto y acelere tareas intensivas. Cada píxel del fractal se calcula de manera independiente, lo que hace posible dividir el trabajo sin que los hilos interfieran entre sí. Experimentando con el número de hilos confirmé mi hipótesis: al aumentar los hilos, el cálculo se aceleraba, aunque también noté que si ponía demasiados, el rendimiento no mejoraba tanto debido a la sobrecarga de coordinación.


--------------------------------- Actividad 4 -------------------------------

Parte 1) SIN HILOS

<img width="665" height="485" alt="image" src="https://github.com/user-attachments/assets/1b30e592-9599-4df4-afb0-d48bd335049d" />
<img width="804" height="723" alt="image" src="https://github.com/user-attachments/assets/fa9e92ab-6557-4d56-98bd-002d0f92eec4" />

En la versión sin hilos, la estructura de datos principal es el vector<Boid> boids dentro de la clase Flock. Ese vector guarda toda la información de los boids y es recorrido en cada actualización para calcular las fuerzas de separación, alineación y cohesión. Como aquí no hay hilos, el acceso al vector lo hace únicamente el hilo principal, tanto para actualizar como para dibujar. En la función Flock::run() el programa recorre el vector y llama a b.run(boids) para cada boid, lo que significa que se están leyendo y escribiendo posiciones y velocidades de todos los elementos. En la función ofApp::draw(), el vector se recorre otra vez, pero esta vez para dibujar cada boid en pantalla. Y cuando arrastro el mouse, Flock::addBoid() añade un nuevo boid al final del vector.

En este escenario sin hilos no hay necesidad de lock() y unlock() porque no existe acceso concurrente: todo ocurre en el mismo flujo. Sin embargo, si imaginamos el mismo código con hilos, ahí sí aparecerían problemas. Por ejemplo, el hilo trabajador podría estar recorriendo el vector para calcular la separación mientras el hilo principal intenta añadir un nuevo boid. Eso invalidaría el iterador y podría provocar un crash. En la versión con hilos, las llamadas a lock() y unlock() evitan ese problema porque garantizan que solo un hilo acceda al vector a la vez. También es importante notar que, aunque los locks aseguran la correctitud, si hubiera muchos hilos intentando acceder al mismo vector, se formarían colas de espera y el paralelismo real se perdería. En este ejemplo solo hay dos hilos (principal y trabajador), así que la contención es baja, pero si se intentara dividir el cálculo entre varios hilos, habría que pensar en estrategias más avanzadas como dividir el espacio en regiones o usar copias temporales de datos.

La diferencia entre el flocking sin hilos y con hilos es clara: en la versión sin hilos todo el cálculo y el dibujo ocurren en el mismo hilo, lo que hace que el frame rate caiga cuando se añaden muchos boids. En la versión con hilos, el cálculo se mueve a un hilo secundario y el principal queda libre para dibujar y responder a eventos, lo que mejora la responsividad. Sin embargo, incluso en la versión con hilos el cálculo dentro del hilo secundario sigue siendo secuencial, así que no hay paralelismo real.

Cuando añado un nuevo boid, la simulación se ralentiza porque el vector se hace más grande y cada boid tiene que calcular sus interacciones con más vecinos. Si añado muchos boids, el costo crece de manera significativa y el FPS baja. En la versión con hilos se añadió un sleep(5) en el hilo trabajador para evitar que el CPU se sature; si se eliminara, el cálculo sería más rápido, pero el procesador podría quedar sobrecargado y la aplicación se sentiría pesada. Comparando ambos enfoques, el sin hilos es más simple pero se bloquea fácilmente, mientras que el con hilos es más eficiente en términos de responsividad, aunque no acelera realmente el cálculo. Si no se usaran lock() y unlock() en la versión con hilos, podrían aparecer condiciones de carrera: resultados inconsistentes, boids que se mueven de manera errática o incluso errores de memoria difíciles de reproducir.


Parte 2) CON HILOS

<img width="1099" height="773" alt="image" src="https://github.com/user-attachments/assets/0f1543f8-320d-463f-bee8-454e565fc325" />
<img width="816" height="541" alt="image" src="https://github.com/user-attachments/assets/6faa15a5-dc7d-4304-b475-617d42c1eaf4" />

En la versión con hilos, la estructura de datos principal sigue siendo el vector<Boid> boids dentro de la clase Flock. La diferencia es que ahora ese vector es accedido por dos hilos distintos: el hilo principal lo usa para dibujar y para añadir nuevos boids, mientras que el hilo secundario lo recorre en threadedFunction() para calcular el movimiento de cada boid. Esto convierte al vector en un recurso compartido y, por lo tanto, en un punto crítico que necesita sincronización.

En la función Flock::threadedFunction(), el hilo trabajador realiza operaciones de actualización sobre el vector: recorre todos los boids, calcula sus fuerzas de flocking y actualiza sus posiciones. En la función ofApp::draw(), el hilo principal recorre el mismo vector pero con otro propósito: dibujar cada boid en pantalla. Y cuando arrastro el mouse, Flock::addBoid() añade un nuevo boid al final del vector. Todas estas operaciones son simultáneas y, sin sincronización, podrían chocar entre sí. Un escenario problemático sería el siguiente: el hilo secundario está recorriendo el vector para calcular la separación entre boids, mientras que el hilo principal recibe un evento de mouseDragged y añade un nuevo boid. El iterador del hilo secundario podría quedar inválido y provocar un error o incluso un crash. Las llamadas a lock() y unlock() evitan este problema porque garantizan que solo un hilo acceda al vector en un momento dado. Si el hilo secundario está recorriendo el vector, el principal debe esperar para añadir un boid, y viceversa.

Sin embargo, también entendí que los locks tienen un costo. Si hubiera muchos hilos intentando acceder al mismo vector, se formarían colas de espera y el paralelismo real se perdería. En este ejemplo solo hay dos hilos, así que la contención es baja, pero si se intentara dividir el cálculo entre varios hilos, habría que pensar en estrategias más avanzadas como dividir el espacio en regiones o usar copias temporales de datos. El ejemplo con hilos es limitado porque solo hay dos hilos: el principal y el trabajador. Eso significa que el cálculo dentro del hilo secundario sigue siendo secuencial, no hay varios hilos procesando subconjuntos de boids en paralelo. Lo que sí se logra es mejorar la responsividad: el hilo principal queda libre para dibujar y responder a eventos, mientras el cálculo ocurre en segundo plano. La aplicación se siente más fluida, aunque el cálculo no sea más rápido.

Si tuviéramos varios hilos calculando el movimiento de los boids, podríamos dividir el conjunto en partes y asignar cada parte a un hilo. El problema sería que cada boid necesita información de sus vecinos, y si esos vecinos están siendo modificados por otro hilo, habría riesgo de condiciones de carrera. La solución pasaría por sincronizar de manera más granular o usar técnicas como copias de datos, pero eso complicaría mucho el código y podría introducir cuellos de botella. Al añadir un nuevo boid, la simulación se ralentiza porque el vector crece y cada boid tiene que calcular sus interacciones con más vecinos. Si añado muchos boids, el costo aumenta y el FPS baja. En la versión con hilos se añadió un sleep(5) en el hilo trabajador para evitar que el CPU se sature; si se eliminara, el cálculo sería más rápido, pero el procesador podría quedar sobrecargado y la aplicación se sentiría pesada.

Comparando ambos enfoques, el sin hilos es más simple pero se bloquea fácilmente, mientras que el con hilos es más eficiente en términos de responsividad. Si no se usaran lock() y unlock(), podrían aparecer condiciones de carrera: resultados inconsistentes, boids que se mueven de manera errática o incluso errores de memoria difíciles de reproducir.

---------------------------------------- Actividad 5 ------------------------------------

<img width="1069" height="800" alt="image" src="https://github.com/user-attachments/assets/6b4ccbb7-a34e-4b23-a2f5-45cf0d466d0a" />
<img width="1013" height="760" alt="image" src="https://github.com/user-attachments/assets/bedcbbbc-fb02-45c5-9579-50194d8828d3" />
<img width="1004" height="780" alt="image" src="https://github.com/user-attachments/assets/16ae5543-da34-46ff-bf68-db9970ba35d7" />

Para implementar el Julia Set interactivo, copié el código del Mandelbrot paralelo y modifiqué la función que calcula cada píxel. La diferencia es que en Mandelbrot z empieza en 0 y c depende del píxel, mientras que en Julia z empieza en la coordenada del píxel y se usa una constante k fija para toda la imagen. En mi función calculateJuliaPixel, inicializo z con las coordenadas del píxel y aplico la iteración z = z^2 + k.

La constante k la hice interactiva mapeando la posición del mouse:
//juliaK.x = ofMap(mouseX, 0, imgWidth, -1.5f, 1.5f);
//juliaK.y = ofMap(mouseY, 0, imgHeight, -1.5f, 1.5f);

De esta forma, al mover el mouse se cambia la parte real e imaginaria de k y se recalcula el fractal.

La estructura de hilos la reutilicé casi sin cambios: cada hilo calcula un bloque de filas de la imagen, igual que en Mandelbrot. Lo único que cambié fue que ahora llaman a calculateJuliaPixel en lugar de calculateMandelbrotPixel.

Para asegurarme de que la imagen se recalculara cuando el mouse se movía, añadí la llamada a startCalculation() dentro de mouseMoved(). Así, cada vez que cambia k, se lanza un nuevo cálculo paralelo y la textura se actualiza.

Incluí capturas mostrando diferentes fractales de Julia generados al mover el mouse. En una se ven estructuras más abiertas y caóticas, y en otra formas más cerradas y simétricas. Esto demuestra cómo pequeñas variaciones en la constante k producen patrones completamente distintos.

El desafío principal fue manejar la interacción: al mover el mouse constantemente se disparan muchos cálculos y hay que coordinar bien los hilos para que no se solapen. También tuve que ajustar el rango de mapeo de k para que los fractales fueran interesantes y no se vieran demasiado vacíos o saturados.
