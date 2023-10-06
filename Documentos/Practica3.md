<div align="center"> <h1> Practica 3 Monitores </h1></div>


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

- [Github con el resto de practicas](https://github.com/Fabian-Martinez-Rincon/Programacion-Concurrente)
- [Ejercicio 1](#ejercicio-1)
- [Ejercicio 2](#ejercicio-2)
- [Ejercicio 3](#ejercicio-3)
- [Ejercicio 4](#ejercicio-4)
- [Ejercicio 5](#ejercicio-5)
- [Ejercicio 6](#ejercicio-6)
- [Ejercicio 7](#ejercicio-7)
- [Ejercicio 7](#ejercicio-7)

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

**CONSIDERACIONES PARA RESOLVER LOS EJERCICIOS:**

- Los monitores utilizan el protocolo signal and continue.
- A una variable condition SÓLO pueden aplicársele las operaciones SIGNAL, SIGNALALL y WAIT.
- NO puede utilizarse el wait con prioridades.
- NO se puede utilizar ninguna operación que determine la cantidad de procesos encolados en una variable condition o si está vacía.
- La única forma de comunicar datos entre monitores o entre un proceso y un monitor es por medio de invocaciones al procedimiento del monitor del cual se quieren obtener (o enviar) los datos.
- No existen variables globales.
- En todos los ejercicios debe maximizarse la concurrencia.
- En todos los ejercicios debe aprovecharse al máximo la característica de exclusión mutua que brindan los monitores.
- Debe evitarse hacer busy waiting.
- En todos los ejercicios el tiempo debe representarse con la función delay.

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 1

Se dispone de un puente por el cual puede pasar un solo auto a la vez. Un auto pide permiso para pasar por el puente, cruza por el mismo y luego sigue su camino.


#### Puente
```c
Monitor Puente
    cond cola;
    int cant= 0;
    Procedure entrarPuente ()
        while ( cant > 0) 
            wait (cola);
        cant = cant + 1;
    end;
    Procedure salirPuente ()
        cant = cant – 1;
        signal(cola);
    end;
End Monitor;

```

#### Auto
```c
Process Auto [a:1..M]
    Puente. entrarPuente (a);
    //el auto cruza el puente
    Puente. salirPuente(a);
End Process;
```



### Parte a

**¿El código funciona correctamente? Justifique su respuesta.**

**RTA** El ejercicio parece estar bien, el primero al tener cant = 0, no entra en el puente e incrementa la cantidad de `cant` en uno. Despues de el primer coche, todos los demas se encolan y se duermen en el `wait`. Al momento de salir un auto, se hace `signal` y se despierta al siguiente auto en la cola.

### Parte b
¿Se podría simplificar el programa? ¿Sin monitor? ¿Menos procedimientos? ¿Sin variable condition? En caso afirmativo, rescriba el código.

**RTA** Se podria simplificar a un solo procedimiento cruzar que cruce el puente. No es necesario la variable condition (`cant`)

#### Puente
```c
Monitor Puente{
    Procedure cruzarPuente (){
        CruzoPuente()
    }
}
```

#### Auto
```c
Process Auto [a:1..M]{
    Puente.cruzarPuente(); //Hace falta pasar el id por pasametro?
}
```

> Queria preguntar si hace falta hacer el codigo por cada pregunta

### Parte c
¿La solución original respeta el orden de llegada de los vehículos? 

No :D

Si rescribió el código en el punto `b)`
**¿esa solución respeta el orden de llegada?**

No :D

> Como corno hago para que sea por orden de llegada :(

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 2

Existen N procesos que deben leer información de una base de datos, la cual es administrada por un motor que admite una cantidad limitada de consultas simultáneas.

---

### Parte a) 

Analice el problema y defina qué procesos, recursos y monitores serán necesarios/convenientes, además de las posibles sincronizaciones requeridas para resolver el problema.

El código presentado es una solución al problema de acceso concurrente a una base de datos que admite un número limitado de consultas simultáneas. 

La solución utiliza un monitor llamado `BaseDeDatos` que tiene una variable de condición `espera` y una variable entera `cant` que representa la cantidad de consultas en curso. El monitor tiene dos procedimientos: `leer()` y `terminarLectura()`. 

El procedimiento `leer()` utiliza un bucle `while` para esperar hasta que haya menos de 5 consultas en curso. Cuando se cumple esta condición, se incrementa la variable `cant`. 

El procedimiento `terminarLectura()` decrementa la variable `cant` y señala la variable de condición `espera`, lo que permite que otro proceso pueda leer de la base de datos.

El proceso `Usuario` utiliza los procedimientos `leer()` y `terminarLectura()` del monitor `BaseDeDatos` para acceder a la base de datos. 

En resumen, esta solución utiliza un monitor para controlar el acceso concurrente a la base de datos y garantizar que no haya más de 5 consultas simultáneas.

###  Parte b) 

Implemente el acceso a la base por parte de los procesos, sabiendo que el motor de base de datos puede atender a lo sumo 5 consultas de lectura simultáneas.


#### Base de Datos

```c
Monitor BaseDeDatos{
    cond espera;
    int cant = 0;
    Procedure leer(){
        while(cant == 5 ){
            wait(espera);
        }
        cant++;
    }
    Procedure terminarLectura(){
        cant--;
        signal(espera);
    }
}
```

#### Usuarios(Que piden consultas)

```c
Process Usuario [u:1..N]{
    BaseDeDatos.leer();
    //Leer
    BaseDeDatos.terminarLectura();
}
```

</td></tr></table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 3

Existen N personas que deben fotocopiar un documento. La fotocopiadora sólo puede ser usada por una persona a la vez. Analice el problema y defina qué procesos, recursos y monitores serán necesarios/convenientes, además de las posibles sincronizaciones requeridas para resolver el problema. Luego, resuelva considerando las siguientes situaciones:

---

### Parte a) 

Implemente una solución suponiendo no importa el orden de uso. Existe una función Fotocopiar() que simula el uso de la fotocopiadora.

#### Fotocopiadora

```c
Monitor Fotocopiadora{
    cond espera;
    int cant = 0;
    Procedure fotocopiar(){
        while(cant == 1 ){
            wait(espera);
        }
        cant++;
    }
    Procedure terminarFotocopiar(){
        cant--;
        signal(espera);
    }
}
```

#### Personas

```c
Process Persona [u:1..N-1]{
    Fotocopiadora.fotocopiar();
    //Fotocopiar
    Fotocopiadora.terminarFotocopiar();
}
```
</td></tr></table>

---

### Parte b) 

Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.

#### Fotocopiadora

```c
Monitor Fotocopiadora{
    cond espera;
    int cant = 0;
    int cantEsperan = 0;

    Procedure fotocopiar(){
        if(cant == 1 ){
            cantEsperan++;
            wait(espera);
        }
        else{
            cant++;
        }
    }
    Procedure terminarFotocopiar(){
        if (cantEsperan > 0){
            cantEsperan--;
            signal(espera);
        }
        else{
            cant--;
        }
    }
}
```

#### Personas

```c
Process Persona [u:1..N-1]{
    Fotocopiadora.fotocopiar();
    //Fotocopiar
    Fotocopiadora.terminarFotocopiar();
}
```

> Usamos cant para representar la cantidad de personas que estan usando la fotocopiadora y cantEsperan para representar la cantidad de personas que estan esperando para usar la fotocopiadora

</td></tr></table>

---

###  Parte c)

Modifique la solución de (b) para el caso en que se deba dar prioridad de acuerdo con la edad de cada persona (cuando la fotocopiadora está libre la debe usar la persona de mayor edad entre las que estén esperando para usarla).

#### Fotocopiadora

```c
Monitor Fotocopiadora{
    ColaPrioridad cola;
    int cant = 0;
    cond espera[N];

    procerdure fotocopiar(int u, int edad){
        if(cant == 1 ){
            cola.encolarOrdenado(u, edad);
            wait(espera[u]);
        }
        else{
            cant++;
        }
    }
    procerdure terminarFotocopiar(){
        if (cola.vacia()){
            cant--;
        }
        else{
            int u = cola.desencolar();
            signal(espera[u]);
        }
    }
}
```

#### Personas

```c
Process Persona [u:1..N-1]{
    edad = Persona.edad();
    Fotocopiadora.fotocopiar(u, edad);
    //Fotocopiar
    Fotocopiadora.terminarFotocopiar();
}
```
</td></tr></table>

---

### Parte d)

Modifique la solución de (a) para el caso en que se deba respetar estrictamente el orden dado por el identificador del proceso (la persona X no puede usar la fotocopiadora hasta que no haya terminado de usarla la persona X-1).


#### Fotocopiadora

```c
Monitor Fotocopiadora{
    cond espera;
    int siguiente = 1;

    Procedure fotocopiar(int u){
        while(u != siguiente ){
            wait(espera);
        }
        siguiente++;
    }

    
    Procedure terminarFotocopiar(){
        signal(espera);
    }
}
```

#### Personas

```c
Process Persona [u:1..N-1]{
    Fotocopiadora.fotocopiar(u);
    //Fotocopiar
    Fotocopiadora.terminarFotocopiar();
}

```


---

### Parte e)

Modifique la solución de (b) para el caso en que además haya un Empleado que le indica a cada persona cuando debe usar la fotocopiadora.


#### Fotocopiadora

```c
Monitor Fotocopiadora{
    cond espera;
    int cant = 0;
    int cantEsperan = 0;

    Procedure fotocopiar(){
        if(cant == 1 ){
            cantEsperan++;
            wait(espera);
        }
        else{
            cant++;
        }
    }
    Procedure terminarFotocopiar(){
        if (cantEsperan > 0){
            cantEsperan--;
            signal(espera);
        }
        else{
            cant--;
        }
    }
}

```


#### Personas

```c
// El proceso deberia tener una senial para esperar que le confirma
// El empleado o como hago esta parte?
Process Persona [id:1..N-1]{ //id es el id de la persona
    Fotocopiadora.fotocopiar();
    //Fotocopiar
    Fotocopiadora.terminarFotocopiar();
}
```

#### Empleado

```c
Process Empleado {
    for (i = 1 to N-1){
        Persona[i].fotocopiar();
    }
}
```



---

### Parte f)

Modificar la solución (e) para el caso en que sean 10 fotocopiadoras. El empleado le indica a la persona cuál fotocopiadora usar y cuándo hacerlo.

<table><tr><td>Fotocopiadora</td><td>Personas</td></tr>
<tr><td>

```c

```
</td><td>

```c

```
</td></tr></table>

Tremenda fiaca hacer este :|

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


## Ejercicio 4

Existen N vehículos que deben pasar por un `puente` de acuerdo con el orden de llegada. 
Considere que el puente no soporta más de 50000kg y que cada vehículo cuenta con su propio peso (ningún vehículo supera el peso soportado por el puente). 


#### Puente

```c
Monitor Puente {
    int capacidad 50000;
    cond espera;
    colaPrioridad colaEspera;

    Procedure entrarPuente(int peso){
        if (peso > capacidad or anot colaEspera.vacia()) {
            colaEspera.encolarOrdenado(peso);
            wait(espera);

            if (not colaEspera.vacia()){
                int peso = colaEspera.desencolar();
                signal(espera);
            }
        }
        capacidad -= peso;
    }

    Procedure salirPuente(int peso){
        capacidad += peso;
        if (not colaEspera.vacia()){
            int peso = colaEspera.desencolar();
            signal(espera);
        }

        }
}
```


#### Vehiuclo

```c
Process Vehiculo [id:1..N]{
    peso = Vehiculo.peso();
    Puente.entrarPuente(peso);
    //Cruzar
    Puente.salirPuente(peso);
}
```

> Consultar

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 5

En un corralón de materiales se deben atender a N clientes de acuerdo con el orden de llegada.

Cuando un cliente es llamado para ser atendido, entrega una lista con los productos que comprará, y espera a que alguno de los empleados le entregue el comprobante de la compra realizada.


### Parte a)
Resuelva considerando que el corralón tiene un único empleado.

#### Corralon

Supongo que un empleado se atiende de a uno a la vez. 

```c
Monitor Corralon{
    cond espera;
    int esperando = 0;
    int dentro = 0;

    Procedure Entrar(){
        if (dentro == 1){
            esperando++;
            wait(espera);
        }
        else{
            dentro = 0;
        }
    }

    Procedure Salir(){
        if (esperando > 0){
            esperando--;
            signal(espera);
        }
        else{
            dentro = 1;
        }
    }
}
```

#### Atencion

// Te lo debo este, alta fiaca
```c
Monitor Atencion{
    Procedure EntregarLista(String lista){

    }
}
```

#### Cliente
```c
Process Cliente [id:1..N]{
    listaProductos = Cliente.listaProductos();

    Corralon.entrar();
    Atencion.comprar(listaProductos);
    Corralon.salir();
}
```

#### Empleado
```c
Procedure Empleado{
    for (i = 1 to N){
        Atencion.esperarLista();
        compronbante = Atencion.entregarComprobante();
        Atencon.entregarComprobante(comprobante);
    }
}
```

### Parte b)
Resuelva considerando que el corralón tiene E empleados (E > 1).

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


## Ejercicio 6
Existe una comisión de 50 alumnos que deben realizar tareas de a pares, las cuales son corregidas por un JTP. Cuando los alumnos llegan, forman una fila. Una vez que están todos en fila, el JTP les asigna un número de grupo a cada uno. Para ello, suponga que existe una función AsignarNroGrupo() que retorna un número “aleatorio” del 1 al 25. Cuando un alumno ha recibido su número de grupo, comienza a realizar su tarea. Al terminarla, el alumno le avisa al JTP y espera por su nota. Cuando los dos alumnos del grupo completaron la tarea, el JTP les asigna un puntaje (el primer grupo en terminar tendrá como nota 25, el segundo 24, y así sucesivamente hasta el último que tendrá nota 1). Nota: el JTP no guarda el número de grupo que le asigna a cada alumno.


#### Entrada

#### Tareas

#### Grupos

#### Alumnos

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 7

En un entrenamiento de fútbol hay 20 jugadores que forman 4 equipos (cada jugador conoce el equipo al cual pertenece llamando a la función DarEquipo()). Cuando un equipo está listo (han llegado los 5 jugadores que lo componen), debe enfrentarse a otro equipo que también esté listo (los dos primeros equipos en juntarse juegan en la cancha 1, y los otros dos equipos juegan en la cancha 2). Una vez que el equipo conoce la cancha en la que juega, sus jugadores se dirigen a ella. Cuando los 10 jugadores del partido llegaron a la cancha comienza el partido, juegan durante 50 minutos, y al terminar todos los jugadores del partido se retiran (no es necesario que se esperen para salir).

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

## Ejercicio 8

Se debe simular una maratón con C corredores donde en la llegada hay UNA máquina expendedoras de agua con capacidad para 20 botellas. Además, existe un repositor encargado de reponer las botellas de la máquina. Cuando los C corredores han llegado al inicio comienza la carrera. Cuando un corredor termina la carrera se dirigen a la máquina expendedora, espera su turno (respetando el orden de llegada), saca una botella y se retira. Si encuentra la máquina sin botellas, le avisa al repositor para que cargue nuevamente la máquina con 20 botellas; espera a que se haga la recarga; saca una botella y se retira.

> Nota: mientras se reponen las botellas se debe permitir que otros corredores se encolen. 