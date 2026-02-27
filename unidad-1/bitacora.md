# Unidad 1

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

Actividad 1  - Sistemas computacionales

"En esta actividad vamos a explorar el concepto del ciclo fetch-decode-execut. El siguiente programa está escrito en el lenguaje ensamblador del computador Hack. Este computador no es un computador comercial, sino un computador didáctico que te permitirá acercarte a los conceptos fundamentales de manera amigable."


<img width="1442" height="912" alt="image" src="https://github.com/user-attachments/assets/4bf3b792-9f7c-4335-a28d-9bf541f3831c" />

<img width="1232" height="746" alt="image" src="https://github.com/user-attachments/assets/65eca3e6-11dd-42e7-9d12-375ab6682353" />

Toma el número 1 y lo guarda en una "caja" llamada registro D, uego toma el número 2 y lo suma con lo que ya está en esa caja (que es 1), así que ahora en la caja D hay un 3, después, guarda ese resultado (el 3) en una posición de la memoria que está en la dirección número 16. Y Finalmente, se queda en un bucle infinito, es decir, no hace nada más, solo espera ahí para que el programa no siga avanzando.


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Actividad 2

"Ahora vamos a analizar juntos el siguiente programa. Este programa tendrá todos los conceptos que vamos investigar en la siguiente fase de la unidad de manera más profunda. En qué nos enfocaremos:

Las partes del computador Hack.
El modelo de programación de la CPU.
La diferencia entre memoria RAM y registros.
Los tipos de instrucciones del lenguaje ensamblador.
Cómo leo el teclado y muestro en pantalla.
Cómo implemento un bucle.
Cómo implemento una condición.
¿Qué es la ALU y qué operaciones realiza?"

<img width="1462" height="921" alt="image" src="https://github.com/user-attachments/assets/cd9bcb1c-5bef-44f5-9b8b-fbe606b9d0f7" />
<img width="1235" height="902" alt="image" src="https://github.com/user-attachments/assets/5c200bec-c1a3-45ae-bf21-37044706e8da" />
<img width="1235" height="921" alt="image" src="https://github.com/user-attachments/assets/60bc2298-e307-4073-aef6-dd2e2d62dad5" />
<img width="1244" height="898" alt="image" src="https://github.com/user-attachments/assets/592b7c64-362c-420f-974b-246c95b7e1a0" />
<img width="1242" height="885" alt="image" src="https://github.com/user-attachments/assets/28e3d7da-bd8f-4498-b63c-2d78f5f779b8" />

El computador Hack del proyecto Nand2Tetris está compuesto por una CPU, memoria RAM y dispositivos de entrada/salida como la pantalla (SCREEN) y el teclado (KBD) ; la CPU contiene la ALU, los registros A y D y el contador de programa (PC) ; el modelo de programación consiste en cargar direcciones en el registro A, realizar operaciones en el registro D y acceder a la memoria mediante M, pasando siempre los cálculos por la ALU ; la diferencia entre RAM y registros es que los registros están dentro de la CPU y son muy rápidos pero pocos, mientras que la RAM está fuera de la CPU, es más grande y almacena datos ; el lenguaje ensamblador Hack tiene solo dos tipos de instrucciones: A-instrucciones (@valor) para cargar direcciones y C-instrucciones para operaciones, asignaciones y saltos ; para leer el teclado se accede a KBD y se verifica si el valor es distinto de cero para saber si una tecla está presionada ; para mostrar en pantalla se escribe en SCREEN usando -1 para encender píxeles y 0 para apagarlos ; un bucle se implementa creando una etiqueta y usando un salto incondicional como 0;JMP para repetir el código ; una condición se implementa realizando una comparación con la ALU y usando saltos condicionales como JGT, JEQ o JNE ; la ALU es la unidad aritmético-lógica que realiza operaciones como suma, resta, negación, AND, OR y comparaciones, y además determina si se deben ejecutar saltos en el programa.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Actividad 3

"Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7."

<img width="1234" height="901" alt="image" src="https://github.com/user-attachments/assets/d6421251-22f6-4cf9-a15a-38119a103ecb" />
<img width="1448" height="911" alt="image" src="https://github.com/user-attachments/assets/4b018571-e10f-4902-a5c3-1d268b4cf8af" />

@5
D=M        // D = RAM[5]

@10
D=D-A      // D = RAM[5] - 10

@MENOR
D;JLT      // Si RAM[5] < 10 saltar a MENOR

// Caso contrario (RAM[5] >= 10)
@7
M=0        // RAM[7] = 0
@FIN
0;JMP

(MENOR)
@7
M=1        // RAM[7] = 1

(FIN)
@FIN
0;JMP      // Bucle infinito para terminar

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Actividad 4 

 "Crea un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12."

 En C# <img width="1699" height="718" alt="image" src="https://github.com/user-attachments/assets/b13b0bfe-6caf-47cd-8b9d-01718e6c2289" />
       <img width="1476" height="339" alt="image" src="https://github.com/user-attachments/assets/40e7cd3b-e288-40fd-bde9-730f80caa652" />
       
 En NAND2Tetris 

   <img width="1244" height="980" alt="image" src="https://github.com/user-attachments/assets/da7e0a33-41b5-4999-ae56-01520ee70cc6" />

TRADUCCION: 
   // suma = 0
@0
D=A
@13        // usando la RAM[13] como variable suma
M=D

// i = 1
@1
D=A
@14        // usando la RAM[14] como variable i
M=D

(LOOP)
// si i > 5 va a END
@14
D=M
@5
D=D-A
@END
D;JGT

// suma = suma + i
@14
D=M
@12
D=D+M
M=D

// i = i + 1
@14
M=M+1

@LOOP
0;JMP

(END)
@13
@12
D=M

(ENDLOOP)
@ENDLOOP
0;JMP


---------------------------------------------------------------------------------------------------------------------------------------
ACTIVIDAD 05

*Sin consultar tus apuntes, el simulador o cualquier otro material, responde con tus propias palabras a las siguientes preguntas. ¡No te preocupes por la perfección! El objetivo es ver qué recuerdas ahora mismo.*

1. Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?

R// El ciclo Fetch-Decode-Execute es como el proceso que sigue la computadora para entender y hacer lo que le pides. Primero, busca la instrucción en la memoria (Fetch), luego la entiende (Decode) y finalmente la ejecuta (Execute). El Program Counter (PC) es como un marcador que le dice a la computadora dónde está la siguiente instrucción para no perderse y seguir el orden correcto. Así, la CPU trabaja paso a paso para que todo funcione bien.

2. ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.

R//  - La instrucción A, que empieza con @, le dice a la computadora a qué lugar ir o qué número usar, como @10 que apunta al número 10. 
     - La instrucción-C es la que hace las operaciones, como copiar o sumar valores, por ejemplo D=M que copia un dato. 
     Básicamente, la instrucción-A señala y la C hace el trabajo con esos datos.

3. Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.

R// - El registro D guarda datos temporales para hacer cálculos o guardar resultados. 
    - El registro A apunta a una dirección de memoria o guarda un número para usar en operaciones. 
    - La ALU es la calculadora  (por decirle de alguana manera) que hace sumas, restas y otras operaciones con los datos que recibe de A y D. Así, juntos permiten que la computadora procese información paso a paso.

4. ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).

R// En Hack, para hacer un salto condicional se usa una instrucción que dice “salta si…” y una etiqueta con la dirección. Por ejemplo, @ETIQUETA y D;JGT significa que si el valor en D es mayor que cero, la computadora salta a donde dice ETIQUETA. Si no, sigue con la siguiente instrucción. Así se controla el flujo según condiciones.

5. ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).

R//  En Hack, un loop se hace con una etiqueta y un salto que repite mientras una condición sea verdadera. Por ejemplo:
  
  @VALOR      // Es la etiqueta "VALOR"                    
D=M         // Guardar el valor de "VALOR" en D
(LOOP)      // Etiqueta que marca el inicio del loop
D=D-1       // Decrementar D en 1
@VALUE
M=D         // Guardar el nuevo valor en VALUE
@LOOP
D;JGT 

En español, por asi decirlo, lo que hace este ejemplo es: se resta 1 a un valor y si sigue siendo mayor que cero, salta al inicio del loop para repetir. Así, el programa sigue restando hasta que el valor llegue a cero y se detiene. 

6. ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?

R// La diferencia entre D=M y M=D, es:
   - D=M significa que se lee de memoria y se guarda en D.
   - M=D significa que el valor se escribe en memoria desde D. En palabras mas tecnicas, significa que el valor que está en el registro D se copia a la memoria en la dirección apuntada.

7. Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).

  - Para leer del teclado en Hack, solo hay que leer el valor que está guardado en una dirección especial que indica qué tecla se presionó.
  - Para pintar un pixel en la pantalla, se escribe un valor en la memoria que controla los puntos de la pantalla. Así, leer y pintar se hacen leyendo o escribiendo en direcciones específicas.
   








## Bitácora de reflexión


