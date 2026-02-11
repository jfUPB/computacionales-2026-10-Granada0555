# Unidad 2

## Bitácora de proceso de aprendizaje

## Bitácora de aplicación 

## Bitácora de reflexión


// Practica 
Ejercicio #8
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

