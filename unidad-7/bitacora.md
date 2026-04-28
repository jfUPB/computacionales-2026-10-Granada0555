# Unidad 7

------------------------------- ACTIVIDAD 1 ----------------------------------------

<img width="1919" height="1104" alt="image" src="https://github.com/user-attachments/assets/17e75a92-f474-4fd6-bf6f-41c956800a7b" />

+ Preguntas que surgen al ver el código
  
¿La versión de OpenGL solicitada en los shaders (#version 460 core) es realmente compatible con la tarjeta gráfica y los drivers instalados?

¿Qué pasos seguiría para ampliar este ejemplo hacia algo más complejo, como añadir colores por vértice, texturas o animaciones?

¿Cómo debería organizar el proyecto a futuro para que sea más claro y escalable: mantener todo en un solo archivo o separar la lógica en módulos distintos?

+ Hipótesis inicial
  
Para que el programa logre dibujar el triángulo necesita tres elementos fundamentales:
    Un contexto válido de OpenGL creado por GLFW y cargado con GLAD.
    Shaders compilados y linkeados correctamente, capaces de transformar los vértices y asignar color.
    Un VAO/VBO (el VBO contiene los datos crudos (los números), el VAO contiene las instrucciones de cómo usar esos datos para dibujar.) configurado con los datos del triángulo y activado al momento de dibujar.
    Al cumplirse estas condiciones, el triángulo aparece en pantalla como se muestra en la evidencia.

-------------------------------- ACTIVIDAD 2 --------------------------------------


Cuando uno empieza con OpenGL en Windows, lo primero que descubre es que no basta con escribir el código del triángulo. Hay varias piezas que tienen que encajar para que todo funcione. Es como armar un rompecabezas: cada biblioteca cumple un rol distinto, y si falta una, el programa no arranca o se queda en negro. GLFW es la que abre la ventana y te da un espacio donde dibujar. Además, se encarga de cosas tan básicas como detectar si presionaste una tecla o moviste el ratón. Sin GLFW, tu programa no tendría “escenario” ni forma de interactuar contigo. opengl32.lib viene con Windows y es como el mínimo necesario para que el compilador entienda que existen funciones de OpenGL. Pero ojo: solo cubre hasta la versión 1.1, que es muy antigua. Es como un diccionario básico que te dice “sí, estas funciones existen”, pero no te da acceso a lo moderno.

Ahí entra GLAD. Piensa en GLAD como el traductor que habla con los drivers de tu tarjeta gráfica y te trae las funciones modernas de OpenGL (3.3, 4.6, etc.). Sin GLAD, tu código compilaría, pero al ejecutar no sabría cómo llamar a esas funciones nuevas. Es el puente entre tu programa y la GPU. GLM es opcional, pero muy útil. Es una biblioteca de matemáticas que te da vectores y matrices listos para usar. Cuando quieras mover tu triángulo, rotarlo o escalarlo, GLM te ahorra escribir toda la matemática a mano. No necesitas librerías externas para usarla porque son solo archivos de cabecera. Y finalmente están los drivers de la GPU, que son los que hacen el trabajo pesado. Ellos implementan las versiones modernas de OpenGL y son los que realmente dibujan en pantalla. Sin los drivers, aunque tengas GLFW y GLAD, no podrías acceder a las funciones avanzadas.

Si tocara decirlo como una historia seria tipo:
GLFW abre el teatro y enciende las luces.
opengl32.lib es el libreto básico que dice “sí, existe una obra llamada OpenGL”.
GLAD es el asistente que trae las instrucciones modernas directamente del director (los drivers).
GLM es el cuaderno de matemáticas que te ayuda a calcular movimientos y transformaciones.
Los drivers de la GPU son los actores que finalmente interpretan todo y hacen que el triángulo aparezca en escena. Así, cuando corres tu programa, cada pieza cumple su papel y el resultado es que el triángulo se dibuja en la ventana.

Ahora de una manera mas tecnica:

+ GLFW es la biblioteca que se encarga de abrir la ventana y manejar el teclado, el ratón y los eventos. Sin ella no tendrías dónde dibujar ni cómo interactuar con tu programa.
+ opengl32.lib viene incluido en Windows y sirve para enlazar las funciones básicas de OpenGL (hasta la versión 1.1). Es como el puente mínimo que permite que tu programa compile, aunque las funciones modernas no están ahí.
+ GLAD es el cargador de funciones modernas de OpenGL. Lo que hace es preguntarle al sistema y a los drivers de tu tarjeta gráfica dónde están las funciones de OpenGL más recientes (por ejemplo, de la versión 3.3 o 4.6) y te las entrega listas para usar en tu código.
+ GLM es opcional, pero muy útil. Es una biblioteca de matemáticas que te da vectores y matrices para manejar transformaciones en 3D. No necesitas librerías externas para usarla porque son solo archivos de cabecera.
+ Los drivers de la GPU son los que realmente implementan las versiones modernas de OpenGL. Sin ellos, aunque tengas GLFW y GLAD, no podrías acceder a las funciones avanzadas.

En conjunto, la relación es así:

+ GLFW abre la ventana y crea el contexto.
+ opengl32.lib permite que el programa compile con las funciones básicas.
+ GLAD carga las funciones modernas desde los drivers de la GPU.
+ GLM te ayuda a hacer las matemáticas necesarias para mover, rotar o escalar tus objetos.
+ Los drivers de la tarjeta gráfica son los que hacen el trabajo pesado de dibujar en pantalla.

----------------------------------- ACTIVIDAD 3 ---------------------------------------------------

  Primero, respondiendo cada pregunta por separado
Cuando me preguntan qué es el contexto OpenGL, lo entiendo como el taller donde se guarda todo lo que necesito para dibujar: shaders, buffers, texturas, configuraciones. Sin ese espacio, las funciones de OpenGL no tendrían dónde aplicarse.

  El rol de GLFW es abrir la ventana y crear ese contexto. Además, me facilita manejar teclado, ratón y eventos. Lo que más valoro es que funciona igual en Windows, Linux o Mac, así no tengo que preocuparme por los detalles de cada sistema operativo.

  OpenGL necesita un contexto porque, sin él, no hay un lugar donde guardar estados ni recursos. Es como pedirle a un pintor que pinte sin darle un estudio ni un lienzo. El contexto conecta mi código con la GPU y le da sentido a las instrucciones.

  El framebuffer lo veo como una hoja invisible donde la GPU pinta cada cuadro antes de mostrarlo en pantalla. Me recuerda a los buffers que estudié en las primeras unidades del curso: espacios temporales de memoria que se usan antes de mostrar el resultado final.

  La relación entre viewport y framebuffer es clara: el framebuffer es toda la hoja, mientras que el viewport es el recorte que decido mostrar. Si no coinciden, la imagen se deforma. Es como elegir qué parte de una foto quiero encuadrar.

  En todo lo analizado, los drivers de la GPU y la GPU misma son los protagonistas. La GPU es el artista que hace los cálculos y dibuja los píxeles, mientras que los drivers son el traductor que conecta mi programa con la GPU y permiten acceder a las funciones modernas.

  El VSync me parece necesario porque sincroniza la velocidad de refresco del programa con la del monitor. Si no lo activo y la imagen es dinámica, aparece el “tearing”: cortes en la imagen porque se muestran cuadros incompletos. Con VSync todo fluye más suave.

  Sobre OpenGL Legacy, sé que es la versión antigua que usaba funciones como glBegin y glEnd. Era más fácil de usar pero menos eficiente. OpenGL moderno, en cambio, se basa en shaders y en el pipeline programable, lo que me da más control y potencia aunque exige más trabajo inicial.

  El shader program es el conjunto de programas que corren en la GPU: vertex y fragment shaders. Son importantes porque definen cómo se transforman los vértices y cómo se colorean los píxeles. Sin ellos, OpenGL moderno no puede dibujar nada.

  Cuando reviso el código setupTriangle(), entiendo que crea los datos del triángulo y los carga en la GPU. El VBO guarda las coordenadas de los vértices y el VAO explica cómo interpretarlas. Juntos permiten que el triángulo se dibuje correctamente.

  En el ciclo principal, noto que en cada frame le digo a OpenGL que use el shader program y el VAO. Si los activo antes del loop, no sería estrictamente necesario repetirlo. Pero hacerlo en cada iteración asegura que, si cambio de shader o VAO, el programa siempre sabe cuál usar. Es útil cuando tengo varias figuras o efectos distintos.

  Ahora, todo junto en una reflexión
Al estudiar el código del triángulo me doy cuenta de que, aunque parece sencillo, en realidad esconde muchos conceptos importantes. El contexto OpenGL es el taller donde todo ocurre; GLFW es el arquitecto que construye ese taller y abre la ventana; el framebuffer es la hoja invisible donde se pinta; y el viewport es el marco que decide qué parte se muestra. La GPU es el artista que hace el trabajo pesado, y los drivers son el traductor que permiten que mi código se convierta en imágenes reales.

  El ciclo principal es el latido del programa: procesa eventos, limpia la pantalla, activa shaders y VAO, dibuja y muestra el resultado. Los shaders son los que dan vida a los vértices y colores, mientras que VAO y VBO organizan los datos para que la GPU sepa cómo usarlos. El VSync asegura que todo fluya sin cortes, y la diferencia entre OpenGL Legacy y moderno me muestra cómo ha evolucionado esta tecnología hacia un modelo más flexible y potente.

  Experimentar con el viewport me hizo ver que pequeños cambios en los parámetros pueden alterar por completo la percepción de la escena. Es como jugar con una lupa sobre una hoja: el triángulo se recorta, se estira o se mueve según los valores que uso. Esa experiencia me recordó que aprender OpenGL no es solo memorizar funciones, sino entender cómo cada pieza se conecta y cómo los cambios afectan el resultado final.


------------------------------------ ACTIVIDAD 4 ------------------------------------------------

Diferencia entre CPU y GPU
Después de ver el video de NVIDIA y recordar lo que aprendí en las primeras unidades, entendí que la CPU es como un trabajador versátil: puede hacer muchas tareas distintas, una tras otra, con gran flexibilidad. La GPU, en cambio, es como un equipo de obreros especializados que trabajan en paralelo. La CPU es buena para lógica y control, mientras que la GPU está diseñada para procesar miles de operaciones gráficas al mismo tiempo. Por eso, cuando se trata de dibujar imágenes o manejar gráficos, la GPU supera ampliamente a la CPU.

¿Cómo funcionan las gráficas en un computador?
El segundo video me ayudó a visualizar el proceso completo. Los gráficos no aparecen mágicamente: hay un pipeline que transforma datos en imágenes. Primero se definen los vértices y las formas, luego se rasterizan (es decir, se convierten en fragmentos), y finalmente se colorean y se iluminan con shaders. La GPU hace todo este trabajo en paralelo, lo que permite que los videojuegos y programas gráficos se vean fluidos y realistas.

¿Cuáles son los tres pasos claves del pipeline de OpenGL?  
Los tres pasos son:

  - Procesamiento de vértices: transformar las coordenadas de los puntos.
  - Rasterización: convertir esas formas en fragmentos que corresponden a píxeles.
  - Procesamiento de fragmentos: decidir el color final de cada fragmento.

¿Qué significa que el pipeline sea programable?  
Antes, OpenGL tenía un pipeline fijo: todo estaba predefinido y no se podía cambiar. Ahora, con el pipeline programable, yo puedo escribir shaders que deciden cómo se transforman los vértices y cómo se colorean los fragmentos. Esto me da libertad creativa y control total sobre el resultado.

¿Cómo describiría la rasterización?  
Es el proceso de convertir las formas geométricas en fragmentos que corresponden a píxeles en la pantalla. Es como pasar de un dibujo vectorial a una imagen hecha de puntos de color.

¿Qué son los fragmentos? ¿Son lo mismo que píxeles?  
Un fragmento es un candidato a convertirse en píxel. Contiene información como color, profundidad y coordenadas. No todos los fragmentos llegan a ser píxeles, porque algunos se descartan en pruebas como el depth test. Por eso no son exactamente lo mismo.

¿Qué problema resuelve el Z-buffer y qué es el depth test?  
El Z-buffer guarda la profundidad de cada fragmento. El depth test compara esa profundidad para decidir qué fragmento se ve y cuál queda oculto detrás. Sin esto, los objetos se dibujarían en desorden y no habría sensación de profundidad.

¿Por qué se presenta el aliasing y qué es el anti-aliasing?  
El aliasing ocurre cuando una línea o borde se ve escalonado porque los píxeles no alcanzan a representar la forma suave. El anti-aliasing suaviza esos bordes mezclando colores, lo que da una apariencia más natural.

¿Qué relación hay entre la iluminación y el fragment shader?  
La iluminación se calcula en el fragment shader, porque ahí se decide el color final de cada fragmento. No siempre es obligatorio incluir iluminación: puedo hacer un shader sin ella, pero el resultado sería plano y poco realista.

¿Qué implica para la GPU tener múltiples fuentes de iluminación?  
Cada fuente de luz añade cálculos extra en el fragment shader. Si hay muchas luces, la GPU tiene que procesar más operaciones por fragmento, lo que puede afectar el rendimiento. Es un equilibrio entre realismo y eficiencia.


Objetos en OpenGL y setupTriangle
En OpenGL todo gira alrededor de objetos. Cada recurso gráfico (buffers, shaders, texturas) se maneja como un objeto con un ID único. Esto permite que la GPU acceda rápido a los datos sin que la CPU tenga que enviarlos cada vez. El contexto de OpenGL es el gran objeto que gestiona todo, y dentro de él se crean otros como el VAO y el VBO. En el ejemplo del triángulo, la función setupTriangle() define los vértices y crea un VAO y un VBO. El VBO guarda los datos de los vértices, mientras que el VAO guarda la configuración de cómo se interpretan esos datos. Con glBufferData se envían los vértices a la GPU, y con glVertexAttribPointer se explica cómo leerlos (posición, tipo de dato, stride, etc.). Finalmente, se habilita el atributo y se hace un “unbind” para evitar problemas.


<img width="1847" height="1110" alt="image" src="https://github.com/user-attachments/assets/9c70e756-e393-4fc2-8eaa-8e9d67f3ebe8" />

Este código crea un VAO y un VBO con tres atributos (posición, color y offset), define tres shaders distintos y en cada draw call activa solo el atributo que corresponde al shader en uso. Así verás tres triángulos renderizados con diferentes lógicas: uno usando posición real, otro usando color como posición “falsa” y otro usando el offset.


------------------------------ ACTIVIDAD 5 ---------------------------------------------------------

<img width="1909" height="1122" alt="Captura de pantalla 2026-04-28 153037" src="https://github.com/user-attachments/assets/d8a23d49-c9eb-40b4-8e6a-0a0faac4621b" />
<img width="1907" height="1146" alt="Captura de pantalla 2026-04-28 153027" src="https://github.com/user-attachments/assets/0237fbbc-f458-4434-9936-81e8236afc83" />
<img width="1912" height="1134" alt="Captura de pantalla 2026-04-28 153020" src="https://github.com/user-attachments/assets/9a0e4440-e3b1-4ae4-ae2c-802116dc7aff" />

- ¿Qué es un uniform?
Un uniform es una variable global dentro del shader que yo puedo establecer desde el código C++ antes de dibujar. A diferencia de los atributos de vértice, que cambian para cada vértice, los uniforms permanecen constantes durante todo un draw call. En este caso, usé un uniform para el offset (posición del triángulo) y otro para el color.

- Proceso de normalización de las coordenadas del mouse
Cuando obtengo la posición del mouse con glfwGetCursorPos, los valores están en píxeles (por ejemplo, 400, 300). Para que sean proporcionales al tamaño de la ventana, divido por el ancho y el alto (SCR_WIDTH, SCR_HEIGHT). Así obtengo valores entre 0 y 1.

Ejemplo: si el mouse está en el centro de la ventana, x = 0.5, y = 0.5.
Esto me permite usar esas coordenadas normalizadas para definir el color del triángulo.

- Normalización a coordenadas de dispositivo (NDC)
OpenGL trabaja en un sistema de coordenadas que va de -1 a 1 en ambos ejes. Por eso, transformo el rango [0,1] a [-1,1].

Fórmula para X: x * 2 - 1

Fórmula para Y: 1 - y * 2 (se invierte porque en GLFW el origen está arriba a la izquierda, mientras que en OpenGL el origen está en el centro con Y positivo hacia arriba).

De esta forma, el triángulo se mueve en la ventana siguiendo el mouse, porque estoy traduciendo las coordenadas del cursor al sistema que OpenGL entiende.

- Relación con el sistema de coordenadas de OpenGL
El sistema de coordenadas de OpenGL (NDC) es el espacio donde todo se dibuja antes de proyectarse en la pantalla. Al normalizar las coordenadas del mouse y transformarlas a NDC, logro que el triángulo se desplace de manera coherente dentro de la ventana. Es como traducir de “idioma píxeles” al “idioma OpenGL”.



