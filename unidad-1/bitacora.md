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






## Bitácora de reflexión
