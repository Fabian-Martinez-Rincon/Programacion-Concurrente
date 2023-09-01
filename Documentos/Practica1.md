<div align="center"> <h1> Practica 1 Variables Compartidas</h1></div>


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

- [Github con el resto de practicas](https://github.com/Fabian-Martinez-Rincon/Programacion-Concurrente)
- [Ejercicio 1](#ejercicio-1)
- [Ejercicio 2](#ejercicio-2)
- [Ejercicio 3](#ejercicio-3)
- [Ejercicio 4](#ejercicio-4)
- [Ejercicio 5](#ejercicio-5)
- [Ejercicio 6](#ejercicio-6)
- [Ejercicio 7](#ejercicio-7)

---

#### Conceptos antes de empezar la practica
- Operacion de grano Grueso

- Operacion de grano Fino

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 1

1.  Para el siguiente programa concurrente suponga que todas las variables están inicializadas en 0 antes de empezar. Indique cual/es de las siguientes opciones son verdaderas: 
- a) En algún caso el valor de x al terminar el programa es 56. 
- b) En algún caso el valor de x al terminar el programa es 22. 
- c) En algún caso el valor de x al terminar el programa es 23

<table>
<tr><td>P1</td><td>P2</td><td>P3</td></tr>
<tr><td>

```java
f (x = 0) then 
 y:= 4*2; 
 x:= y + 2;
```
</td><td>

```java
If (x > 0) then 
  x:= x + 1; 
```
</td><td>

```java
x:= (x*3) + (x*2) + 1; 
```
</td></tr>
</table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 2

Realice una solución concurrente de grano grueso (utilizando <> y/o <await B; S>) para el siguiente problema. Dado un número N verifique cuántas veces aparece ese número en un arreglo de longitud M. Escriba las pre-condiciones que considere necesarias.

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


#### Ejercicio 3

Dada la siguiente solución de grano grueso:

a) Indicar si el siguiente código funciona para resolver el problema de Productor/Consumidor con un buffer de tamaño N. En caso de no funcionar, debe hacer las modificaciones necesarias

##### Variables compartidas
```java
int cant = 0;
int pri_ocupada = 0;
int pri_vacia = 0;
int buffer[N]; 
```

<table>
<tr><td>Productor</td><td>Consumidor</td></tr>
<tr><td>

```java
Process Productor::{
  while (true){ //produce elemento 
    <await (cant < N); cant++>
    buffer[pri_vacia] = elemento;
    pri_vacia = (pri_vacia + 1) mod N;
  } 
}
```
</td><td>

```java
Process Consumidor::{
  while (true) { 
    <await (cant > 0); cant-- > 
    elemento = buffer[pri_ocupada]; 
    pri_ocupada = (pri_ocupada + 1) mod N; 
    //consume elemento 
  } 
}
```
</td></tr>
</table>

b) Modificar el código para que funcione para C consumidores y P productores.

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 4

Resolver con 
- SENTENCIAS AWAIT (<> y <await B; S>).

Un sistema operativo mantiene 5 instancias de un recurso almacenadas en una cola, cuando un proceso necesita usar una instancia del recurso la saca de la cola, la usa y cuando termina de usarla la vuelve a depositar.

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 5

En cada ítem debe realizar una solución concurrente de grano grueso (utilizando <> y/o <await B; S>) para el siguiente problema, teniendo en cuenta las condiciones indicadas en el item. Existen N personas que deben imprimir un trabajo cada una.

---

a) Implemente  una  solución  suponiendo  que  existe  una  única  impresora  compartida  por todas las personas, y las mismas la deben usar de a una persona a la vez, sin importar el orden. Existe una función Imprimir(documento) llamada por la persona que simula el uso de la impresora. Sólo se deben usar los procesos que representan a las Personas.

---

b) Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.

---

c) Modifique la solución de (a) para el caso en que se deba respetar el orden  dado por el identificador  del  proceso  (cuando  está  libre  la  impresora,  de  los  procesos  que han solicitado su uso la debe usar el que tenga menor identificador). 

---

d) Modifique la solución de (b) para el caso en que además hay un proceso Coordinador que le indica a cada persona que es su turno de usar la impresora

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 6

Dada la siguiente solución para el Problema de la Sección Crítica entre dos procesos (suponiendo que tanto SC como SNC son segmentos de código finitos, es decir que terminan 
en algún momento), indicar si cumple con las 4 condiciones requeridas

##### Variable compartida
```java
int turno = 1; 
```

<table>
<tr><td>P1</td><td>P2</td></tr>
<tr><td>

```java
Process SC1::{ 
  while (true) { 
    while (turno == 2) skip;  
    SC; 
    turno = 2; 
    SNC; 
  } 
}
```
</td><td>

```java
Process SC2::  
{ while (true) 
      {   while (turno == 1) skip;  
           SC; 
           turno = 1; 
           SNC; 
       } 
}
```
</td></tr>
</table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


#### Ejercicio 7

Desarrolle una solución de grano fino usando sólo variables compartidas (no se puede usar las sentencias await ni funciones especiales como TS o FA). En base a lo visto en la clase 3 de teoría, resuelva el problema de acceso a sección crítica usando un proceso coordinador. 

En este caso, cuando un proceso SC[i] quiere entrar a su sección crítica le avisa al coordinador, y espera a que éste le dé permiso. Al terminar de ejecutar su sección crítica, el proceso SC[i] le avisa al coordinador. 

>Nota: puede basarse en la solución para implementar barreras con “Flags y coordinador” vista en la teoría 3. 






