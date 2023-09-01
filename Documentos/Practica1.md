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

<div align='center'>

#### Conceptos antes de empezar la practica</div>

**Intrucción atomica**: que solo el proceso que la esta ejecutando la puede modificar (explucion mutua)

```python
<await (B); sentencias>
```

- Hasta que la condicion `B` no sea verdadera, el proceso que la esta ejecutando, va a estar bloqueado (o en espera), no la pasa de largo, no es lo mismo que un `if` por ejemplo
- Una vez que es verdadero, se ejecuta la sentencia que esta asociada a esa condicion, estas sentencias se ejecutan de forma atomica
- Cuando se detecta que es verdadero, empieza la "atomicidad"

```python
<sentencias>
```

El protocolo de entrada seria `<` y el protocolo de salida seria `>` y `sentencias` seria la sección critica (zona en la que no pueden estar mas de un proceso a la vez)

- No existe ningun tipo de orden a medida de que los procesos estan esperando a que se libere.

```python
<await (B);>
```

El proceso que esta ejecutando esta instruccion, se bloquea hasta que la condicion `B` sea verdadera

<div align='center'>

#### Ejemplos de la practica</div>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 1

Para el siguiente programa concurrente suponga que todas las variables están inicializadas en 0 antes de empezar. Indique cual/es de las siguientes opciones son verdaderas: 

***a) En algún caso el valor de x al terminar el programa es 56.***

Se tienen que ejecutar los procesos P1, P2 y P3 en ese orden y completos para que x valga 56

***b) En algún caso el valor de x al terminar el programa es 22.***

- Se ejecuta `P3` solo `x*3` incompleto (x= 0*3 = 0)
- Se ejecuta `P2` Completo dejando x=20
- Se ejecuta lo que queda de `P3` dejando x= 10*2 + 1 = 21
- Por ultimo se ejecuta `P2` completo dejando x= 21 + 1 = 22

***c) En algún caso el valor de x al terminar el programa es 23***

- Se ejecuta `P3` solo `x*3` incompleto (x= 0*3 = 0)
- Se ejecuta `P1` Completo dejando x=10
- Se ejecuta `P2` Completo dejando x=11
- Se ejecuta lo que queda de `P3` dejando x= 11*2 + 1 = 23


<table>
<tr><td>P1</td><td>P2</td><td>P3</td></tr>
<tr><td>

```java
f (x = 0) then 
 y:= 4*2; 
 x:= y + 2;
//x = 8 + 2 = 10

```
</td><td>

```java
If (x > 0) then 
  x:= x + 1; 
//x = 10 + 1 = 11
```
</td><td>

```java
x:= (x*3) + (x*2) + 1; 
//x = (11*3) + (11*2) + 1 = 56

```
</td></tr>
</table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 2

Realice una solución concurrente de grano grueso (utilizando <> y/o <await B; S>) para el siguiente problema. Dado un número N verifique cuántas veces aparece ese número en un arreglo de longitud M. Escriba las pre-condiciones que considere necesarias.

```java
1 int total = 0;
2 int arr[M];

3 Process Arrays[id: 0..P-1] {
4     int suma = 0;
5     int parte = M / P;
6     int extra = 0;
7     int inicio = id * parte;
  
8     if (id == P-1) {
9         extra = M mod P;
10    }

11    for (i = inicio; i < inicio + parte + extra; i++) {
12        if (arr[i] == N) {
13            suma++;
14        }
15    }

16    if (suma != 0) {
17        <total += suma>
18    }
19 }
```
***Ejemplo***

Supongamos que tienes un arreglo de 100 elementos (`M = 100`) y tienes 4 procesos (`P = 4`).

- Cada proceso manejaría 100 / 4 = 25 elementos del arreglo.

En este caso, la variable `parte` sería 25.

***Nota sobre `extra`***

La variable `extra` maneja el caso en que `M` no es un múltiplo exacto de `P`. Si tienes, por ejemplo, un arreglo de 103 elementos y 4 procesos, entonces `parte = 103 / 4 = 25`, y tendrías un `extra = 103 mod 4 = 3`. Este `extra` se añade al último proceso para asegurar que todos los elementos del arreglo se procesen.



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



El código parece intentar resolver el problema del productor-consumidor utilizando un buffer circular, pero hay varios problemas potenciales:

No hay garantía de exclusión mutua cuando se accede a la variable compartida `buffer`. Esto puede llevar a condiciones de carrera.

<table>
<tr><td>Productor</td><td>Consumidor</td></tr>
<tr><td>

```java
Process Productor::{
  while (true){ //produce elemento 
    <await (cant < N); cant++
    buffer[pri_vacia] = elemento;>
    pri_vacia = (pri_vacia + 1) mod N;
  } 
}
```
</td><td>

```java
Process Consumidor::{
  while (true) { 
    <await (cant > 0); cant--
    elemento = buffer[pri_ocupada];>
    pri_ocupada = (pri_ocupada + 1) mod N; 
    //consume elemento 
  } 
}
```
</td></tr>
</table>


***b) Modificar el código para que funcione para C consumidores y P productores.*** Preguntar

En caso de que tengamos N procesos independiente de cada tipo, tenemos que proteger el valor de N, ya que podemos estar usando la variable N en diferentes procesos. 

<table>
<tr><td>Productor</td><td>Consumidor</td></tr>
<tr><td>

```java
Process Productor [id:0..P-1]:::{
  while (true){ //produce elemento 
    <await (cant < N); cant++
    buffer[pri_vacia] = elemento;
    pri_vacia = (pri_vacia + 1) mod N;>
  } 
}
```
</td><td>

```java
Process Consumidor [id:0..C-1]:::{
  while (true) { 
    <await (cant > 0); cant--
    elemento = buffer[pri_ocupada];
    pri_ocupada = (pri_ocupada + 1) mod N;>
    //consume elemento 
  } 
}
```
</td></tr>
</table>

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






