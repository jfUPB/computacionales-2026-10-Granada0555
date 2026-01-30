# Unidad 1

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

Actividad 4 - Sistemas computacionales

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

