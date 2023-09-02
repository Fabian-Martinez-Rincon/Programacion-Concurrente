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

---

#### Ejemplos de la practica

##### Ejercicio 1
Se tiene un salón con cuatro puertas por donde entran los alumnos a un examen.
Cada puerta lleva la cuenta de los que entraron por ella y a su vez se lleva la cuenta del total de personas en el salón.

```java
int Total = 0;
Process Puerta[id: 0..3]{ 
  int Parcial = 0;
  while (true){ 
    //esperar llegada
    Parcial = Parcial + 1;
    <Total= Total + 1>;
  }
}
```

##### Ejercicio 2

Hay un docente que les debe tomar examen oral a 30 alumnos (de a uno a la vez) de acuerdo al orden dado por el Identificador del proceso

***Variables Compartidas***

```java
int Actual = -1; 
bool Listo = False, Ok = false;
```

<table>
<tr><td>Alumno</td><td>Docente</td></tr>
<tr><td>

```java
Process Alumno [id: 0..29]{ 
  <await (Actual == id)>;
  Ok = true;
  //Rinde el examen
  <await (Listo)>;
  Listo = false;
}
```
</td><td>

```java
Process Docente{ 
  for i = 0..29 {
    Actual = i<await (Ok)>; 
    Ok = false;
    //Toma el examen
    Listo = true;
    <await (not Listo)>;
  }
}
```
</td></tr>
</table>


##### Ejercicio 3

Un cajero automático debe ser usado por ***N personas*** de a uno a la vez y según
el orden de llegada al mismo. En caso de que llegue una persona anciana, la
deben dejar ubicarse al principio de la cola.

> Vamos a suponer que existe una estructura de datos “colaEspecial” con una función “Agregar(edad, id)” que dependiendo de ese valor lo inserta la tupla al principio o al final de la cola; y existe una función “Sacar” que devuelve el id de quien está al principio en la cola.

```java
//Variables compartidas
colaEspecial C;
int Siguiente = -1;

Process Persona [id: 0..N-1]{ 
  int edad = ....;

  <if (Siguiente = -1) 
    Siguiente = id
  else 
    Agregar(C, edad, id)>;

  <await (Siguiente == id)>;
  //Usa el cajero
  <if (empty(C)) 
    Siguiente = -1
  else 
    Siguiente = Sacar(C)>;
}
```

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

Resolver con:

```java
SENTENCIAS AWAIT (<> y <await B; S>).
```

Un sistema operativo mantiene 5 instancias de un recurso almacenadas en una cola, cuando un proceso necesita usar una instancia del recurso la saca de la cola, la usa y cuando termina de usarla la vuelve a depositar.

```java
Inicializar colaEspecial C con 5 instancias de recurso;

Process Consumidor[id: 0..N-1] {
  Declarar variable T "rec";
  while(true) {
    <await !empty(C); //Espera a que haya un recurso disponible
      rec = Sacar(C)
    >
    Usar recurso (alguna acción con "rec");
    <Agregar(C, rec)>
  }
}
```

- **1)** Cada proceso `Consumidor` funciona en un bucle infinito (`while(true)`).
- **2)** El proceso espera (`AWAIT`) hasta que la cola `C` no esté vacía (`!empty(C)`).
- **3)** Una vez que la cola tiene al menos un recurso, el proceso saca (`Sacar`) un recurso de la cola y lo asigna a la variable `rec`.
- **4)** El recurso se usa (`usar recurso`).
- **5)** Después de usar el recurso, se agrega (`Agregar`) de nuevo a la cola `C` para que otros procesos puedan usarlo.


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 5

En cada ítem debe realizar una solución concurrente de grano grueso `(utilizando <> y/o <await B; S>)` para el siguiente problema:

- Existen `N` personas que deben imprimir un trabajo cada una.

---

a) Implemente una solución suponiendo que existe una única impresora compartida por todas las personas, y las mismas la deben usar de a una persona a la vez, sin importar el orden. Existe una función Imprimir(documento) llamada por la persona que simula el uso de la impresora. Sólo se deben usar los procesos que representan a las Personas.

```java
// Indica si la impresora está libre o no
bool libre = true;
Process Persona[id: 0..N-1] {
  while(true) {
    <await libre; 
      libre = false; 
      Imprimir(documento); 
      libre = true
    >
  }
}
```


- **1)** La variable `libre` se inicializa en `true`, lo que indica que la impresora está disponible.
- **2)** Cada persona entra en un bucle infinito para imprimir documentos.
- **3)** Usamos la sentencia `<await libre; libre = false; Imprimir(documento); libre = true>` para hacer que el proceso espere hasta que `libre` sea `true`. Una vez que eso sucede, la variable `libre` se establece en `false` para bloquear la impresora, se realiza la acción de imprimir (`Imprimir(documento)`), y luego se libera la impresora estableciendo `libre` nuevamente en `true`.

Con este diseño, nos aseguramos de que solo una persona a la vez pueda utilizar la impresora.

---

b) Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.

```java
cola C;
bool libre = true; 
int sig=-1;
Process Persona[id:0..P-1]::{
  <if (sig=-1) 
    sig=id
  else 
    Agregar(C,id)>;
  <await (sig==id)>;
  <await libre; 
    libre = false;
    Imprimir(documento);
    libre = true
  >
  <if(empty(C) 
     sig=-1;
  else 
     sig=Sacar(C)>;
}
```

- **Inicialización**: La cola `C` está vacía, `libre` es `true`, y `sig` es `-1`.
- **Cuando una Persona llega**: 
  - Si `sig` es `-1`, entonces esta Persona se convierte en la siguiente (**sig = id**).
  - De lo contrario, se añade su `id` a la cola `C`.
- **Esperando para imprimir**: Cada Persona espera hasta que su `id` sea igual a `sig`.
- **Imprimiendo**: Una vez que `sig` es igual al `id` de la Persona y la impresora está libre (`libre = true`), la Persona imprime su documento.
- **Liberar la cola**:
  - Si la cola `C` está vacía, `sig` se vuelve `-1`.
  - Si no, `sig` se convierte en el `id` que está en el frente de la cola, y se saca ese `id` de la cola.

---

c) Modifique la solución de (a) para el caso en que se deba respetar el orden dado por el identificador del proceso (cuando está libre la impresora, de los procesos que han solicitado su uso la debe usar el que tenga menor identificador)

```java
cola C;
bool libre = true; 
int sig=-1;
Process Persona[id:0..P-1]::{
  <if (sig=-1) 
    sig=id
  else 
    AgregarOrdenado(C,id)>; //A chequear
  <await (sig==id)>;
  <await libre; 
    libre = false; 
    Imprimir(documento); 
    libre = true
  >
  <if(empty(C) 
    sig=-1;
  else 
    sig=Sacar(C)>;
}
```

Esta solución es muy similar a la anterior, pero con una diferencia clave:

- En lugar de añadir el `id` al final de la cola, se inserta en un lugar que mantenga el orden ascendente de los `id` en la cola. Por lo tanto, el `id` más pequeño siempre estará en el frente.

---

d) Modifique la solución de (b) para el caso en que además hay un proceso Coordinador que le indica a cada persona que es su turno de usar la impresora

#### Variables compartidas

```java
libre=true;
int siguiente=-1
```

<table>
<tr><td>Personas</td><td>Cordinador</td></tr>
<tr><td>

```java
Process Persona[1..N]::{
  <Agregar(C,id);>
  <await (siguiente==id)>;
  <await libre; 
     libre = false; 
     Imprimir(documento); 
     libre = true
   >
}
```
</td><td>

```java
Process Coordinador::{
  int sig
  while(true){
    <await !empty(C); sig=Sacar(C)>
    <await libre; 
      libre=false>
    siguiente=sig
    <libre=true>
    }
 }
```

</td></tr>
</table>

**Inicialización**: `libre` es `true` y `siguiente` es `-1`.

*Personas*
- **Cuando una Persona llega**: Añade su `id` a la cola `C`.
- **Esperando para imprimir**: Cada Persona espera hasta que su `id` sea igual a `siguiente`.
- **Imprimiendo**: Una vez que `siguiente` es igual al `id` de la Persona y **libre = true**, la Persona imprime su documento.

*Coordinador*
- **Elegir siguiente Persona**: 
  - El Coordinador espera hasta que la cola `C` no esté vacía y la impresora esté libre.
  - Saca el `id` del frente de la cola y lo asigna a `siguiente`.


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

#### Ejercicio 6

Dada la siguiente solución para el Problema de la Sección Crítica entre dos procesos (suponiendo que tanto SC como SNC son segmentos de código finitos, es decir que terminan en algún momento), indicar si cumple con las 4 condiciones requeridas

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
Process SC2::{ 
  while (true) {
    while (turno == 1) skip;
      SC; 
      turno = 1; 
      SNC; 
  } 
}
```
</td></tr>
</table>



#### 1. Exclusión Mutua ✔️

En este código, la variable compartida `turno` se utiliza para garantizar que solo un proceso puede estar en su sección crítica (`SC`) en un momento dado. Si `turno` es `1`, entonces `P1` puede entrar en su `SC`, y `P2` no puede (y viceversa). Así que esta condición se cumple.

#### 2. Ausencia de Deadlock (o Livelock)✔️

No hay deadlock en este diseño, ya que siempre hay un `turno` específico en el que uno de los procesos puede entrar en su `SC`. En el peor de los casos, tendrían que esperar a que el otro proceso termine su `SC` para entrar en la suya. Por lo tanto, esta condición también se cumple.

#### 3. Ausencia de Demora Innecesaria ❌

La ausencia de demora innecesaria podría no cumplirse completamente. Imagina un escenario en el que el proceso P1 entra y sale de su SC muy rápidamente en comparación con P2. P2 tendría que esperar a que P1 complete su SC y cambie el turno, incluso si P1 pudiera funcionar eficazmente en su sección no crítica. Esto podría considerarse una demora "innecesaria" para P2.

#### 4. Eventual Entrada ✔️

El diseño asegura que si un proceso intenta entrar en su `SC`, eventualmente podrá hacerlo. Esto se debe a que el "turno" cambia después de que un proceso sale de su `SC`, permitiendo al otro proceso entrar en su `SC`. Entonces, esta condición también se cumple.


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


#### Ejercicio 7

Desarrolle una solución de grano fino usando sólo variables compartidas (no se puede usar las sentencias await ni funciones especiales como TS o FA). En base a lo visto en la clase 3 de teoría, resuelva el problema de acceso a sección crítica usando un proceso coordinador. 

En este caso, cuando un proceso SC[i] quiere entrar a su sección crítica le avisa al coordinador, y espera a que éste le dé permiso. Al terminar de ejecutar su sección crítica, el proceso SC[i] le avisa al coordinador. 

>Nota: puede basarse en la solución para implementar barreras con “Flags y coordinador” vista en la teoría 3. 

##### Variables compartidas

```java
bool libre= true;
int arribo[1:n]]=([n] false)
```

<table><tr><td>Procesos</td><td>Cordinador</td></tr>
<tr><td>

```java
Process Proceso[id:1..N]:: {
  while (true) {
    arribo[id] = true
    while (arribo[id]) { skip };
    SC
    libre=true;
    SNC
  }
}
```
</td><td>

```java
Process Coordinador:: {
  while(true) {
    for [i=1 to n st arribo[i]==true]{
      while (not libre) skip;
      libre=false;
      arribo[i] = false;
    }
  }
}
```
</td></tr></table>

#### Procesos
- Cada proceso avisa que quiere entrar a su sección crítica (`SC`) poniendo `arribo[id] = true`.
- Espera hasta que el coordinador ponga `arribo[id] = false`.
- Después de ejecutar su `SC`, pone `libre = true`.

#### Coordinador
- Busca procesos que hayan llegado (`arribo[i] == true`).
- Espera a que el recurso esté `libre`.
- Pone `libre = false` y `arribo[i] = false` para permitir al proceso entrar a su `SC`.

**Pros**: 
- Simple de entender.

**Contras**: 
- Se podrían generar condiciones de carrera porque no hay mecanismos de exclusión mutua reales para proteger la variable `libre` y el arreglo `arribo`.

### Otra solución

```java
int next=-1;
int arribo[1:n]=([n] false)
```

<table>
<tr><td>Procesos</td><td>Cordinador</td></tr>
<tr><td>

```java
Process Proceso[id:1..N]:: {
  while (true){
    arribo[id] = true
    while (id != next) { skip };
    SC
    next = -1;
    SNC
  }
}
```
</td><td>

```java
Process Coordinador:: {
  while(true){
    for [i=1 to n st arribo[i]==true]{
      while (next!=-1) skip;
      arribo[i] = false;
      next = i;
    }
  }
}
```
</td></tr>
</table>

#### Procesos
- Cada proceso avisa que quiere entrar a su `SC` poniendo `arribo[id] = true`.
- Espera hasta que `next = id`.
- Después de su `SC`, pone `next = -1`.

#### Coordinador
- Busca procesos que hayan llegado (`arribo[i] == true`).
- Espera hasta que `next = -1`.
- Pone `arribo[i] = false` y `next = i`.

**Pros**: 
- Más estructurada que la primera.

**Contras**: 
- Al igual que la primera solución, podría tener condiciones de carrera.

> Ambas soluciones intentan ofrecer una implementación de grano fino pero no garantizan la exclusión mutua en el acceso a las variables compartidas, lo que podría llevar a condiciones de carrera. Podrían funcionar en un ambiente ideal donde estas condiciones de carrera no ocurran, pero no son soluciones robustas para todos los escenarios posibles.