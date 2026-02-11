# Unidad 2

## Bitácora de proceso de aprendizaje

## Bitácora de aplicación 

## Bitácora de reflexión


// Practica 
Ejercicio #8

1). 
<img width="1864" height="908" alt="Captura de pantalla 2026-02-11 163455" src="https://github.com/user-attachments/assets/35e1dff9-e2c3-4812-8e77-9b1281930301" />
<img width="1861" height="910" alt="Captura de pantalla 2026-02-11 163446" src="https://github.com/user-attachments/assets/78311cf6-4d51-4e2a-9fcc-ebbe9774bd29" />
<img width="1245" height="912" alt="Captura de pantalla 2026-02-11 163427" src="https://github.com/user-attachments/assets/3c7a5952-c22f-499d-9ab4-ebe9b4b368c1" />
<img width="1866" height="970" alt="Captura de pantalla 2026-02-11 163320" src="https://github.com/user-attachments/assets/3aeff743-73ae-4a25-94d4-e4126515628a" />

// MAIN
// a = 10

@10
D=A
@16
M=D

// b = 20
@20
D=A
@17
M=D

// Pasar argumentos (direcciones)

@16
D=A
@R0
M=D      // R0 = &a

@17
D=A
@R1
M=D      // R1 = &b

// Guardar dirección de retorno
@RETURN_MAIN
D=A
@R15
M=D

// Llamar a swap
@SWAP
0;JMP

// RETORNO A MAIN

(RETURN_MAIN)


// FUNCIÓN SWAP

(SWAP)

// tmp = *pa
@R0
A=M      // A = dirección de a
D=M      // D = *pa
@R13
M=D      // tmp en R13

// *pa = *pb
@R1
A=M      // A = dirección de b
D=M      // D = *pb

@R0
A=M      // A = dirección de a
M=D      // *pa = *pb

// *pb = tmp
@R13
D=M      // D = tmp

@R1
A=M      // A = dirección de b
M=D      // *pb = tmp

// Return
@R15
A=M

// Fin del programa
(END)
@END
0;JMP

//--------------------------------------------------------------------------------------------------------------------------

2). 



<img width="1246" height="913" alt="Captura de pantalla 2026-02-11 165946" src="https://github.com/user-attachments/assets/4769e17f-90d9-4ff7-82bc-f67c053d10f1" />
<img width="1222" height="902" alt="Captura de pantalla 2026-02-11 165923" src="https://github.com/user-attachments/assets/a6b16c12-a329-4641-b3bb-e625224818ed" />


(start)

// sumResult = 0
@sumResult
M=0


// Crear arreglo arr[]


// arr[0] = 10
@10
D=A
@arr
M=D

// arr[1] = 15
@15
D=A
@arr
A=A+1
M=D

// arr[2] = 2
@2
D=A
@arr
A=A+1
A=A+1
M=D

// arr[3] = 3
@3
D=A
@arr
A=A+1
A=A+1
A=A+1
M=D

// arr[4] = 50
@50
D=A
@arr
A=A+1
A=A+1
A=A+1
A=A+1
M=D



// Pasar argumentos


@arr
D=A
@R0
M=D        // R0 = base

@5
D=A
@R1
M=D        // R1 = size

// Guardar retorno
@returnFromCalSum
D=A
@R15
M=D

@calSum
0;JMP


(returnFromCalSum)

// Guardar resultado
@R0
D=M
@sumResult
M=D

@fin
(fin)
0;JMP




// FUNCIÓN calSum

(calSum)

// sum = 0
@0
D=A
@R13
M=D

// i = 0
@0
D=A
@R14
M=D


(loop)

// if i >= size salir
@R14
D=M
@R1
D=D-M
@endLoop
D;JGE


// D = base
@R0
D=M

// D = base + i
@R14
D=D+M

// A = base + i
A=D

// D = *(parr+i)
D=M

// sum += D
@R13
M=D+M

// i++
@R14
M=M+1

@loop
0;JMP


(endLoop)

// return sum
@R13
D=M
@R0
M=D

@R15
A=M
0;JMP


