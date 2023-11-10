> La practica 1 no entra en el parcial  

## Lo que rescato de la practica 1

- Mientras menos variables compartidas, menos secciones criticas voy a tener que proteger
- Trabajar siempre con variables locales y cuando termino, volcar el resultado sobre la variable compartida.
- Si sabes la cantidad de iteraciones que tiene que hacer un proceso, se usa un for, no un while
- Si las variables compartidas, las modifica solo un proceso y los demas solo la leen, no hace falta < proteger esa variable >
- Identificamos los procesos

## Resumen Practica 2 Semaforos

- Siempre se tienen que inicializar los semaforos (sem mutex=1 o sem expera[5] = ([5] 1 ))