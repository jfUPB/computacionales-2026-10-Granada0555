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

