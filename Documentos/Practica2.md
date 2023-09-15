<style>
    img {
        width: 100%;
        height:20px
    }
</style>

# Práctica 2 – Semáforos

CONSIDERACIONES PARA RESOLVER LOS EJERCICIOS:
- Los semáforos deben estar declarados en todos los ejercicios.
- Los semáforos deben estar inicializados en todos los ejercicios.
- No se puede utilizar ninguna sentencia para setear o ver el valor de un semáforo.
- Debe evitarse hacer busy waiting en todos los ejercicios.
- En todos los ejercicios el tiempo debe representarse con la función delay


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


- [Ejercicio 1](#ejercicio-1)
- [Ejercicio 2](#ejercicio-2)
- [Ejercicio 3](#ejercicio-3)
- [Ejercicio 4](#ejercicio-4)
- [Ejercicio 5](#ejercicio-5)
- [Ejercicio 6](#ejercicio-6)
- [Ejercicio 7](#ejercicio-7)
- [Ejercicio 8](#ejercicio-8)
- [Ejercicio 9](#ejercicio-9)
- [Ejercicio 10](#ejercicio-10)
- [Ejercicio 11](#ejercicio-11)
- [Ejercicio 12](#ejercicio-12)

---

### Ejemplo 1

Hay C chicos y hay una bolsa con caramelos que nunca se vacía. Los chico de a UNO van sacando de a UN caramelo y lo comen. Los chicos deben llevar la cuenta de cuantos caramelos se han tomado de la bolsa.

```c
int cant = 0;
sem mutex = 1;
Process Chico[id: 0..C-1]{ 
    while (true){ 
        P(mutex);
        -- tomar caramelo
        cant = cant + 1;
        V(mutex); 
        -- comer caramelo
    } 
}
```

### Ejemplo 2

Hay C chicos y hay una bolsa con caramelos limitada a N caramelos. Los chico de a UNO van sacando de a UN caramelo y lo comen. Los chicos deben llevar la cuenta de cuantos caramelos se han tomado de la bolsa

```c
int cant = 0;
sem mutex = 1;
Process Chico[id: 0..C-1]{
    P(mutex);
    while (cant < N){
        -- tomar caramelo
        cant = cant + 1;
        V(mutex); 
        -- comer caramelo
        P(mutex);
    } 
    V(mutex);
}
```

### Ejemplo 3

Hay C chicos y hay una bolsa con caramelos limitada a N caramelos administrada por UNA abuela. Cuando todos los chicos han llegado llaman a la abuela, y a partir de ese momento ella N veces selecciona un chico aleatoriamente y lo deja pasar a tomar un caramelo.

```c
int contador = 0; bool seguir = true;
sem mutex = 1, espera_abuela = 0, barrera = 0, espera_chicos[C] = ([C] 0), listo = 0;
```

<table><td>

```c
Process Chico[id: 0..C-1]{ 
    int i;
    P(mutex);
    contador = contador + 1;
    if (contador == C) { 
        for i = 1..C → V(barrera);
        V(espera_abuela); 
    }
    V(mutex);
    P(barrera);
    P(espera_chicos[id]);
    while (seguir){ 
        --tomar caramelo
        V(listo);
        --comer caramelo 
        P(espera_chicos[id]);
    }
}
```
</td><td>

```c
Process Abuela{
    int i, aux;
    P(espera_abuela);
    for i = 1..N { 
        aux = (rand mod C);
        V(espera_chicos[aux]);
        P(listo);
    }
    seguir = false;
    for aux = 0..C-1 → V(espera_chicos[aux]);
}
```
</td>
</table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

### Ejercicio 1

Existen N personas que deben ser chequeadas por un detector de metales antes de poder ingresar al avión.

**a)** Analice el problema y defina qué procesos, recursos y semáforos serán necesarios/convenientes, además de las posibles sincronizaciones requeridas para resolver el problema.

N personas (), Detector de metales (recurso), mutex (semaforos), exclusion mutua (sincronizacion)

**b)** Implemente una solución que modele el acceso de las personas a un detector (es decir, si el detector está libre la persona lo puede utilizar; en caso contrario, debe esperar).

```c
sem mutex = 1
Process Persona[id:1..N]{
    //Llega al detector
    P(mutex)
    //Se detecta
    V(mutex)
    //Sube al avión
}
```


**c)** Modifique su solución para el caso que haya tres detectores. 

```c
sem mutex = 3
Process Persona[id:1..N]{
    //Llega al detector
    P(mutex)
    //Se detecta
    V(mutex)
    //Sube al avión
}
```

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 2

Un sistema de control cuenta con 4 procesos que realizan chequeos en forma colaborativa. Para ello, reciben el historial de fallos del día anterior (por simplicidad, de tamaño N). De cada fallo, se conoce su número de identificación (ID) y su nivel de gravedad (0=bajo, 1=intermedio, 2=alto, 3=crítico). Resuelva considerando las siguientes situaciones:

**a)** Se debe imprimir en pantalla los ID de todos los errores críticos (no importa el orden).

```c

```

**b)** Se debe calcular la cantidad de fallos por nivel de gravedad, debiendo quedar los resultados en un vector global.

```c

```

**c)** Ídem b) pero cada proceso debe ocuparse de contar los fallos de un nivel de gravedad determinado.

```c

```

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 3

Un sistema operativo mantiene 5 instancias de un recurso almacenadas en una cola.

Además, existen P procesos que necesitan usar una instancia del recurso. Para eso, deben sacar la instancia de la cola antes de usarla. Una vez usada, la instancia debe ser encolada nuevamente

```c
sem mutex = 1, espera = 5
cola T recursos[5]
Process Proceso[id:1..P]{
    while(true){
        P(espera)
            P(mutex)
                pop(recursos,rec)
            V(mutex)
                usar(rec)
            P(mutex)
                push(recursos,rec)
            V(mutex)
        V(espera)
    }
}
```

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 4

Suponga que existe una BD que puede ser accedida por 6 usuarios como máximo al mismo tiempo. Además, los usuarios se clasifican como usuarios de prioridad alta y usuarios de prioridad baja. Por último, la BD tiene la siguiente restricción:
- no puede haber más de 4 usuarios con prioridad alta al mismo tiempo usando la BD.
- no puede haber más de 5 usuarios con prioridad baja al mismo tiempo usando la BD.

> Indique si la solución presentada es la más adecuada. Justifique la respuesta.

```pascal
Var
    sem: semaphoro := 6;
    alta: semaphoro := 4;
    baja: semaphoro := 5;
```

<table>
<tr><td>

```c
Process Usuario-Alta [I:1..L]::{
    P (sem);
    P (alta);
    //usa la BD
    V(sem);
    V(alta);
}
```
</td><td>

```c
Process Usuario-Baja [I:1..K]::{ 
    P (sem);
    P (baja);
    //usa la BD
    V(sem);
    V(baja);
}
```
</td></tr>

</table>

No, no es la mas adecuada. P(alta) y P(baja) deberian ir antes de P(sem), ya que evita demora innecesaria al preguntar si hay primero espacio para gente de alta/baja antes de reservar el espacio para entrar. Lo mismo ocurre con V(alta) y V(baja), deberian ir antes de V(sem) ya que causo demora innecesaria si libero un usuario antes de liberar alta o baja

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 5

En una empresa de logística de paquetes existe una sala de contenedores donde se preparan las entregas. Cada contenedor puede almacenar un paquete y la sala cuenta con capacidad para N contenedores. Resuelva considerando las siguientes situaciones:




---

**a)** La empresa cuenta con 2 empleados: un empleado Preparador que se ocupa de preparar los paquetes y dejarlos en los contenedores; un empelado Entregador que se ocupa de tomar los paquetes de los contenedores y realizar la entregas. Tanto el Preparador como el Entregador trabajan de a un paquete por vez.

```c
sem cantidad= N
sem hayPaquetes= 0
sem mutex= 1;
Paquete llenos[N]
int front= 0,rear = 0;
```

<table><td>

```c
Process Preparador{
    Paquete paquete
    while(true){
        //prepara paquete
        P(cantidad)
            P(mutex)
                buffer[rear]= paquete
            V(mutex)
        rear= (rear + 1) mod N;
        V(hayPaquetes)
    }
}
```
</td><td>

```c
Process Entregador{
    Paquete paquete
    while(true){
        P(hayPaquetes)
            P(mutex)
                paquete= buffer[front]
            V(mutex)
            front= (front+1) mod N
        V(cantidad)
    }
}
```
</td></table>


---

**b)** Modifique la solución a) para el caso en que haya P empleados Preparadores.

<table><td>

```c
Process Preparador[id:0..P-1]{
    Paquete paquete
    while(true){
        //prepara paquete
        P(cantidad)
            P(mutex)
                buffer[rear]= paquete
                rear= (rear + 1) mod N;
            V(mutex)
        V(hayPaquetes)
    }
}
```
</td><td>

```c
Process Entregador{
    Paquete paquete
    while(true){
        P(hayPaquetes)
            P(mutex)
                paquete= buffer[front]
            V(mutex)
            front= (front+1) mod N
        V(cantidad)
    }
}
```
</td></table>

---

**c)** Modifique la solución a) para el caso en que haya E empleados Entregadores.

<table><td>

```c
Process Preparador{
    Paquete paquete
    while(true){
        prepara paquete
        P(cantidad)
            P(mutex)
                buffer[rear]= paquete
            V(mutex)
            rear= (rear + 1) mod N;
        V(hayPaquetes)
    }
}
```
</td><td>

```c
Process Entregador[id:0..E-1]{
    Paquete paquete
    while(true){
        P(hayPaquetes)
            P(mutex)
                paquete= buffer[front]
                front= (front+1) mod N
            V(mutex)
        V(cantidad)
    }
}
```
</td></table>

---

**d)** Modifique la solución a) para el caso en que haya P empleados Preparadores y E empleadores Entregadores.

<table><td>

```c
Process Preparador[id:0..P-1]{
    Paquete paquete
    while(true){
        prepara paquete
        P(cantidad)
            P(mutex)
                buffer[rear]= paquete
                rear= (rear + 1) mod N;
            V(mutex)
        V(hayPaquetes)
    }
}
```
</td><td>

```c
Process Entregador[id:0..E-1]{
    Paquete paquete
    while(true){
        P(hayPaquetes)
            P(mutex)
                paquete= buffer[front]
                front= (front+1) mod N
            V(mutex)
        V(cantidad)
    }
}
```
</td></table>


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20999px">


### Ejercicio 6

Existen N personas que deben imprimir un trabajo cada una. Resolver cada ítem usando
semáforos:

**a)** Implemente una solución suponiendo que existe una única impresora compartida por todas las personas, y las mismas la deben usar de a una persona a la vez, sin importar el orden. Existe una función Imprimir(documento) llamada por la persona que simula el uso de la impresora. Sólo se deben usar los procesos que representan a las Personas.

```c
sem mutex= 1;
Process Persona[id:0..P-1]{
    P(mutex)
        Imprimir(documento)
    V(mutex)
}
```

**b)** Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.

```c
sem mutex= 1;
sem T espera[P]= ([P] 0)
cola c;
boolean libre= true;

Process Persona[id:0..P-1]{
    int aux;
    P(mutex)
    if(libre) {
        libre= false; 
        V(mutex)
    }
    else{
        push(c,id)
        V(mutex)
        P(espera[id])
    }
    Imprimir(documento)
    P(mutex)
    if(empty(c)) 
        libre= true
    else { 
        pop(c,aux)); 
        V(espera[aux]) 
    }
    V(mutex)
}
```


**c)** Modifique la solución de (a) para el caso en que se deba respetar estrictamente el orden dado por el identificador del proceso (la persona X no puede usar la impresora hasta que no haya terminado de usarla la persona X-1).

```c
sem mutex= 1;
sem T espera[P]= ([P] 0)
boolean libre= true;

Process Persona[id:0..P-1]{
    if id != 0 {
        P(espera[id])
    }
    imprimir(documento)
    if id != P-1{
        // el 0 no entra de vuelta igual Preguntar
        V(espera[id+1]) 
     }
}
```



**d)** Modifique la solución de (b) para el caso en que además hay un proceso Coordinador que le indica a cada persona que es su turno de usar la impresora.

```c
sem mutex= 1;
sem T espera[P]= ([P] 0)
sem termine = 1
boolean libre= true;
```


<table><td>

```c
Process Persona[id:0..P-1]{
    int aux;
    P(mutex)
        push(c,id)
    V(mutex)
    V(coord)
    P(espera[id])
        Imprimir(documento)
    V(termine)
}
```
</td><td>

```c
int aux;
Process Coordinador{
    while(true){
        P(coord);
        P(mutex);
            pop(c,aux);
        V(mutex);
        P(termine)
        V(espera[aux]);
    }
}
```
</td> </table>

**e)** Modificar la solución (d) para el caso en que sean 5 impresoras. El coordinador le indica a la persona cuando puede usar una impresora, y cual debe usar. 

```c
sem coord= 0, mutex= 1, espera= ([P], 0), termine = 5
cola T c[P]; cola Impresoras impresoras[5]; sem impMutex= 1;
```


<table><td>

```c
Process Persona[id:0..P-1]{
    Impresora imp;
    int aux;
    P(mutex)
        push(c,id)
    V(mutex)
    
    V(coord)
    P(espera[id])
    P(impMutex)
        pop(impresoras,imp)
        V(impMutex)
            Imprimir(documento,imp)
        P(impMutex)
        push(impresoras,imp)
    V(impMutex)
    V(termine)
}
```
</td><td>

```c
int aux;
Process Coordinador{
while(true){
    P(coord);
    P(mutex);
        pop(c,aux);
    V(mutex);
    P(termine)
    V(espera[aux]);
}
}
```
</td> </table>



<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' >


### Ejercicio 7

Suponga que se tiene un curso con 50 alumnos. Cada alumno debe realizar una tarea y existen 10 enunciados posibles. Una vez que todos los alumnos eligieron su tarea, comienzan a realizarla. Cada vez que un alumno termina su tarea, le avisa al profesor y se queda esperando el puntaje del grupo, el cual está dado por todos aquellos que comparten el mismo enunciado. Cuando un grupo terminó, el profesor les otorga un puntaje que representa el orden en que se terminó esa tarea de las 10 posibles.

> Nota: Para elegir la tarea suponga que existe una función elegir que le asigna una tarea a un alumno (esta función asignará 10 tareas diferentes entre 50 alumnos, es decir, que 5 alumnos tendrán la tarea 1, otros 5 la tarea 2 y así sucesivamente para las 10 tareas).

```c
int eligiocount = 50
A= 50
sem eligio = 0, mutex = 1, barrera= 0, terminoGrupo = 0, alus = 0;
sem grupoMutex[10] = 0;
sem corrigio[10] = 0;
sem barreraGrupo[10] = 0;
sem mutexColas = 1
int cantGrupo[10] = 5
cola colaGrupos,
```

```c
Process Alumno[id:0..A-1]{
    int idGrupo = elegir()
    P(mutex)
        eligiocount = eligiocount-1
        if eligiocount == 0 {
            V(barrera);
        }
    V(mutex)
    P(alus)
    //hacer tarea
    P(grupoMutex[idGrupo])
        cantGrupo[idGrupo]= cantGrupo[idGrupo]-1;
        if (cantGrupo[idGrupo]== 0){
            V(grupoMutex[idGrupo])
            P(mutexColas)
            push(colaGrupos,idGrupo)
            V(mutexColas)
            V(terminoGrupo)
        }else{
            V(grupoMutex[idGrupo])
    }
    P(corrigio[idGrupo])
}
```

```c
Process Profesor{
    P(barrera)
    int orden= 1;
    for i= 1 to A do{
        V(alus)
    }
    for j= 1 to 10 do{
        P(terminoGrupo)
        P(mutexColas)
            pop(colaGrupos,idGrupo)
        V(mutexColas)

        nota[idGrupo]= orden;
        orden++;

        for j= 1 to 5 do {
            V(corrigio[idGrupo])
        }
    }
}
```


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 8

Una fábrica de piezas metálicas debe producir T piezas por día. Para eso, cuenta con E empleados que se ocupan de producir las piezas de a una por vez (se asume T>E). La fábrica empieza a producir una vez que todos los empleados llegaron. Mientras haya piezas por fabricar, los empleados tomarán una y la realizarán. Cada empleado puede tardar distinto tiempo en fabricar una pieza. Al finalizar el día, se le da un premio al empleado que más piezas fabricó.

```c
int llegaron = 0, piezas[E] = ([E]0)
sem esperando = 0, mutex = 1
Process Empleado[id:0..E-1]{
    // llega a la fabrica
    bool ultimo;
    P(mutex)
        llegaron++;
        if (llegaron==E){
            for i= 1 to E do { 
                V(esperando) 
            }
        }
    V(mutex)
    P(esperando)
    P(mutex)
        while(T>0){
            T--;
            if(T==0) {
                ultimo==true
            }
            V(mutex)
            fabricar_pieza(materiales,mano_de_obra)
            piezas[id]++;
            P(mutex)
        }
    V(mutex);
    if (ultimo){
        dar(premio,max(piezas).pos) -- max devuelve pos y cantidad
        for i = 0 to E-1{ -- Sino el premiado puede ya haber finalizado
        V(salida)
        }
    }
    P(salida)
}
```

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 9

Resolver el funcionamiento en una fábrica de ventanas con 7 empleados (4 carpinteros, 1 vidriero y 2 armadores) que trabajan de la siguiente manera:

- Los carpinteros continuamente hacen marcos (cada marco es armando por un único carpintero) y los deja en un depósito con capacidad de almacenar 30 marcos.
- El vidriero continuamente hace vidrios y los deja en otro depósito con capacidad para 50 vidrios.
- Los armadores continuamente toman un marco y un vidrio (en ese orden) de los depósitos correspondientes y arman la ventana (cada ventana es armada por un único armador).

```c
sem marcos = 30, vidrios = 50,
hayMarcos = 0, hayVidrios = 0
depoMarco = 1, depoVidrio = 1
cola<Marco> colaMarcos; cola<Vidrio> colaVidrios;
```

<table><td>

```c
Process Carpintero[id:0..3]{
    while(true) {
        hace marco // preguntar adentro o afuera
        P(marcos)
        P(depoMarco)
            push(colaMarcos,marco);
        V(depoMarco)
        V(hayMarcos)
    }
}
```

</td><td>

```c
Process Vidriero{
    while (true){
        hace vidrio // preguntar adentro o afuera
        P(vidrios)
        P(depoVidrio)
        push(colaVidrios,vidrio);
        V(depoVidrio)
        V(hayVidrios)
    }
}
```
</td></table>

```c
Process Armador[id:0..1]{
    while (true){
        P(hayMarcos)
        P(depoMarco)
            pop(colaMarcos,marco)
        V(depoMarco)
        V(marcos)
        P(hayVidrios)
        P(depoVidrio)
            pop(colaVidrios,vidrio)
        V(depoVidrio)
        V(vidrios)
        //arma ventana
    }
}
```


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 10

A una cerealera van T camiones a descargarse trigo y M camiones a descargar maíz. Sólo hay lugar para que 7 camiones a la vez descarguen, pero no pueden ser más de 5 del mismo tipo de cereal. Nota: no usar un proceso extra que actué como coordinador, resolverlo
entre los camiones.

```c
sem trigo= 5,maiz= 5,lugares= 7;
```

<table><td>

```c
process CamionTrigo [id:0..T-1]{
    while(true){
        P(trigo)
        P(lugares)
        descargar(carga)
        V(trigo)
        V(lugares)
    }
}
```

</td><td>

```c
process CamionMaiz [id:0..M-1]{
    while (true){
        P(maiz)
            P(lugares)
            descargar(carga)
            V(maiz)
        V(lugares)
    }
}
```
</td></table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 11

En un vacunatorio hay un empleado de salud para vacunar a 50 personas. El empleado de salud atiende a las personas de acuerdo con el orden de llegada y de a 5 personas a la vez. Es decir, que cuando está libre debe esperar a que haya al menos 5 personas esperando, luego vacuna a las 5 primeras personas, y al terminar las deja ir para esperar por otras 5. Cuando ha atendido a las 50 personas el empleado de salud se retira. 

> Nota: todos los procesos deben terminar su ejecución; asegurarse de no realizar Busy Waiting; suponga que el empleado tienen una función VacunarPersona() que simula que el empleado está vacunando a UNA persona. 

```c
 sem haycinco = 0;
int cant = 5, P = 5, idGrupo= 0
cola grupo[10]

```

<table><td>

```c
Process Persona[id:0..P-1]{
    P(mutex)
        cant--; // protege esto
        push(grupo[idGrupo],id)
        if(cant==0){
            idGrupo++;
            cant= 5;
            V(haycinco)
        }
    V(mutex)
    P(vacuno[id])
    //se va
}
```

</td><td>

```c
int listo[5];
int i,atendidos;
int idGrupoRevisado= 0;

Process Empleado{
    for (atendidos = 0; atendidos < 10; atendidos++){
        P(haycinco)
        for i:=0 to 4 {
            listo[i]= pop(grupo[idGrupoRevisado])
            Vacunar(persona)
        }
        for i:=0 to 4{
            V(vacuno[listo[i]])
        }
        idGrupoRevisado++;
    }
    se va
}
```
</td></table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">


### Ejercicio 12

Simular la atención en una Terminal de Micros que posee 3 puestos para hisopar a 150 pasajeros. En cada puesto hay una Enfermera que atiende a los pasajeros de acuerdo con el orden de llegada al mismo. Cuando llega un pasajero se dirige al puesto que tenga menos gente esperando. Espera a que la enfermera correspondiente lo llame para hisoparlo, y luego se retira. Nota: sólo deben usar procesos Pasajero y Enfermera.
Además, suponer que existe una función Hisopar() que simula la atención del pasajero por
parte de la enfermera correspondiente


```c
int P = 150, hisopados = 0
cola<Persona> puestos[3]
int cant_puestos[3] = ([3]0)
sem espera[P] = ([P]0), hayPaciente[3] = 0
```

<table><td>

```c
Process Pasajero[id:0..P-1]{
    int min, min_cant = -1;
    P(mutex)
        for i= 0;i<3;i++{
            if cant_puestos[i]<min_cant{
                min_cant= cant_puestos[i]
                min= i
            }
        }
        P(mutexCola[min])
            push(id, puestos[min])
        V(mutexCola[min])
        cant_puestos[min]++
    V(mutex)
    V(haypaciente[min])
    P(espera[id])
    //se va
}
```

</td><td>

```c
Process Enfermera[id:0..2]{
    P(hayPaciente[id])
    P(mutexHisopados)
    while(hisopados < 150){
        hisopados++
        V(mutexHisopados)
        if (hisopados==150) {
            for(i= 0 to 2){
                V(hayPaciente[i])
            }
        }
        P(mutexCola[id])
            pop(idpaciente,puestos[id])
        V(mutexCola[id])
        Hisopar(idpaciente)
        V(espera[idpaciente])
        P(hayPaciente[id])
        P(mutexHisopados)
    }
    V(mutexHisopados)
}
```
</td></table>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">
