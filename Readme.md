<div align="center"> <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&duration=1200&pause=1000&color=F78E23&center=true&width=435&lines=Programación Concurrente"/></div>

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">

- [Explicaciones Teoricas](https://youtube.com/playlist?list=PLH8A0IjFldaGLATsgRdmPBtiNcp5KmAHo)
- [✅ Practica 1 Variables Compartidas](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica1.html)
- [✅ Practica 2 Semáforos](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica2.html)
- [✅ Practica 3 Monitores](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica3.html)
- [Con esto aprobe el segundo parcial que contiene la practica 4 y 5](/Documentos/practica4-5.md)

## Resumen para recuperar el primer pacial

### Resumen Semaforos

- Siempre que tengamos variables compartidas usamos mutex (como la cola y contadores)
- Si usamos las variables compartidas en un bucle, tenemos que hacer un mutex, al principio, y al final del bucle, y dentro del bucle una vez que terminamos de usar los recursos compartidos, hacemos un **V(mutex)**, hacemos lo que tenemos que hacer de forma local, y despues hacemos un **P(mutex)** al final (para esperar a que se libere antes de volver a entrar al bucle)
- Cuando identificamos que se ejecuta una accion despues de que lleguen varios procesos, tenemos que usar una barrera. (En toda la barrera se usa el mutex de principio a fin nada mas)<br>
    **Lo que esta dentro del proceso**
    ```c
    P(mutex)
    contador = contador + 1;
    if(contador == C){
        for i = 1..C do{
            V(barrera)
        }
    }
    V(mutex)
    P(barrera)
    ```
- Cuando tenemos dos procesos, uno que administra y otro que consume, el **V(Mutex)** final lo hace el proceso que administraba, y el **P(Mutex)** inicial lo hace el proceso que consume. **Mutex** en este caso podria ser un semafor que dica **procesoEspera[id]** si necesitamos que ese proceso espera a ser llamado. Y el **V(Mutex)** No lo haria sobre el semaforo **procesoEspera[id]** sino que necesitariamos otro semaforo para indicar que termino y avisar al coordinador como por ejemplo **V(listo)**
- Siempre que indique algun **tipo de orden de llegada**, vamos a usar una cola. Cada vez que hagamos una operacion de push y pop sobre esa cola, vamos a usar Mutex.
- Si usamos una cola, tenemos que esperar a que tenga elementos para poder usarla por lo que usamos un semaforo normal **pedidosCliente** o algo asi, y del lado del proceso administrador, es un **P(pedidosCliente)** antes de comenzar
- Si en una parte tenemos varios procesos que esperan un resultado especifico, voy a tener un array de algun tipo de dato a elegir para referir el recurso a ese proceso en especifico

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/e5dde3d0-4e6a-4425-821d-4196bbdd38d2)

```c
sem Mutex=1;
process Persona[id: 0..N-1]{
    P(Mutex);
    UsarDetector();
    V(Mutex)
}
```

```c
sem Mutex=3;
process Persona[id: 0..N-1]{
    P(Mutex);
    UsarDetector();
    V(Mutex)
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/b64e82fb-809a-42c9-9f44-97b8ff36bda2)

```c
sem instancias = 5
cola recursos;

process Proceso[id:0..P-1]{
    recurso r
    while (true){
        P(instancias)
        P(Mutex)
        r = recursos.pop()
        V(Mutex)

        UsarRecurso(r)

        P(Mutex)
        recursos.push(r)
        V(Mutex)

        V(instancias)
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/fc6f60a7-2d9b-4768-b112-da1785c3598e)

```c
text Contenedores[N]
sem Capacidad = N
sem Paquetes=0


process Preparador{
    Paquete p
    int indicePreparador=0

    while (true){
        
        Preparar(p)

        P(Capacidad)
        P(Mutex)
        Contenedores[indicePreparador]=p
        V(Mutex)
        indicePreparador=(indicePreparador + 1) mod N
        V(Paquetes)
    }
}
process Entregador{
    Paquete p
    int indiceEntregador=0

    while (true){

        P(Paquetes)
        P(Mutex)
        p = Contenedores[indiceEntregador]
        V(Mutex)
        EntregarPaquete(p)
        indiceEntregador = (indiceEntregador + 1) mod P
        V(Capacidad)
    }
}
```

B)
En  este  caso al tener P preparadores la variable indicePreparador deja de ser local y pasa a ser compartida por los P Preparadores ya que si fuera local, varios procesos podrian estar trabajando sobre el mismo indice y no podrian trabajar por separado.

IndicPreparador ahora va dentro de Mutex porque es una variable compartida ahora

```c
text Contenedores[N]
sem Capacidad = N
sem Paquetes=0
int indicePreparador=0

process Preparador[id:0..P-1]{
    Paquete p

    while (true){
        
        Preparar(p)

        P(Capacidad)
        P(Mutex)
        Contenedores[indicePreparador]=p
        indicePreparador=(indicePreparador + 1) mod N
        V(Mutex)
        V(Paquetes)
    }
}
process Entregador{
    Paquete p
    int indiceEntregador=0

    while (true){

        P(Paquetes)
        P(Mutex)
        p = Contenedores[indiceEntregador]
        V(Mutex)
        EntregarPaquete(p)
        indiceEntregador = (indiceEntregador + 1) mod P
        V(Capacidad)
    }
}
```

```c
text Contenedores[N]
sem Capacidad = N
sem Paquetes=0
int indicePreparador=0

process Preparador[id:0..P-1]{
    Paquete p

    while (true){
        
        Preparar(p)

        P(Capacidad)
        P(Mutex)
        Contenedores[indicePreparador]=p
        indicePreparador=(indicePreparador + 1) mod N
        V(Mutex)
        V(Paquetes)
    }
}

int indiceEntregador=0
process Entregador[id: 0..E-1]{
    Paquete p

    while (true){

        P(Paquetes)
        P(Mutex)
        p = Contenedores[indiceEntregador]
        indiceEntregador = (indiceEntregador + 1) mod P
        V(Mutex)

        EntregarPaquete(p)
        V(Capacidad)
    }
}
```

D) Esta es basicamente los otros dos juntos

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/156e9ed9-4b87-4c93-82f9-311dcd3bea05)

```c
sem Impresora=1
process Persona[id:0..N-1]{
    text documento

    P(Impresora)
    ImprimirDocumento(documento)
    V(Impresora)
}
```
b)

```c
sem Mutex=1
Cola c
boolean ocupada=false
sem EsperaPersona[N] = ([N] 0)

process Persona[id:0..N-1]{
    text documento
    int idSiguiente

    documento = generarDocumento()

    P(Mutex)
    if (not ocupada){
        ocupada = true
        V(Mutex)
    }
    else {
        c.push(id) //No hace falta encolar el documento porque es local
        V(Mutex)
        P(EsperaPersona[id])
    }

    ImprimirDocumento(documento)

    P(Mutex)
    if (not empty(c)){
        idSiguiente = c.pop()
        V(EsperaPersona[idSiguiente])
    }
    else{
        ocupada = true
    }
    V(Mutex)

}
```

c)

```c
sem EsperaPersona[N] = ([N] 0)
EsperaPersona[0] = 1


process Persona[id:0..N-1]{
    text documento

    documento = generarDocumento()

    P(EsperaPersona[id])
    ImprimirDocumento(documento)
    V(EsperaPersona[id++])

}
```

D)

```c
sem Mutex=1
Cola c
sem EsperaPersona[N] = ([N] 0)
sem Impresora = 0

process Persona[id:0..N-1]{
    text documento

    documento = generarDocumento()

    P(Mutex)
    c.push(id,documento)
    V(Mutex)
    V(pedidosPersona)
    P(EsperaPersona[id])

    ImprimirDocumento(documento)

    V(Impresora)
}

process Coordinador{
    int idPersona;

    while (true){
        P(pedidosPersona)
        P(Mutex)
        idPersona = c.pop()
        V(Mutex)

        V(EsperaPersona[idPersona])
        P(Impresora)
    }
}
```

E)

```c
sem Mutex=1
Cola c
sem EsperaPersona[N] = ([N] 0)

process Persona[id:0..N-1]{
    text documento

    documento = generarDocumento()

    P(Mutex)
    c.push(id,documento)
    V(Mutex)
    V(pedidosPersona)
    P(EsperaPersona[id])
    
    nroImpresora = impresoraAsignada[id]

    usarImpresora(nroImpresora, documento)

    V(Impresora[nroImpresora])
}

sem Impresora[5] = ([5] 0)
int impresoraAsignada[N];
sem impresorasTotales = 5

process Coordinador{
    int idPersona;
    int nroImpresora

    while (true){
        P(pedidosPersona)

        P(impresorasTotales)
        //Busca en  los semaforos el primero con valor 0
        nroImpresora = impresoraLibre(Impresoras)

        P(Mutex)
        idPersona = c.pop()
        V(Mutex)

        ImpresoraAsignada[idPersona] = nroImpresora
        
        V(EsperaPersona[idPersona])
    }
}
```


![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/9d705b69-2c45-48fc-800f-9b1db7bc30e3)
![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/5dd12e19-1bcb-4bd1-803d-1eca76c13cb0)

```c
int tareasAsignadas = 0
sem Mutex = 1
sem alumnosListos = 0


process Alumno[id:0..49]{
    text tareaAsignada

    P(entrarAula)
    tareaAsignada = Tareas[id]
    
    P(Mutex)
    tareasAsignadas = tareasAsignadas + 1
    if (tareasAsignadas = 50){
        V(alumnosListos)
    }
    V(Mutex)
    P(Barrera)

    RealizarTarea(tareaAsignada)
    tareasTerminadas = tareaAsignada
    V(alguienTermino)
    P(esperoPuntaje[nroGrupo])
}

sem entrarAula = 0
sem grupos[10] = ([10] 0)

process Profesor{
    int i
    for i in 0..49 {
        Tareas[i] = elegir()
    }
    for i in 0..49 {
        V(entrarAula)
    }

    P(alumnosListos)
    V(Barrera)

    int idAlumno
    while (true){
        P(alguienTermino)
        idGrupo = quienTermino(tareasTerminadas)
        //Que fiaca continuar pero se deberia usar una cola cuando terminen
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/90f8ff11-9b18-4e22-be3c-a9eb1ab73c35)

```c
int llegaron = 0
sem TodosTerminaron = 0;
sem llegaronTodos = 0
int totalPiezas=0


process Empleado[id:0..E-1]{
    Pieza p

    P(Mutex)
    llegaron = llegaron + 1
    if llegaron = E {
        V(llegaronTodos)
    }
    V(Mutex)

    P(TodosTerminaron)
    
    int piezasHechas = 0;
    P(Mutex)
    while (totalPiezas != T){
        totalPiezas =  totalPiezas + 1
        V(Mutex)

        hacerPieza(p)
        piezasHechas = piezasHechas + 1
        P(Mutex)
    }
    V(Mutex)
    
    piezasProducidasEmpleado[id] = piezasHechas;

    V(NoHayPiezas)

    P(seEntregoPremio)

    if (idMax = id){
        TomarPremio()
    }
    
}

sem seEntregoPremio = 0

int idMax = -1
sem NoHayPiezas = 0
int piezasProducidasEmpleados[E] = ([E] 0)

process Coordinador{

    P(llegaronTodos)
    int i
    for i in 1..E {
        V(TodosTerminaron)
    }

    P(NoHayPiezas)

    idMax = empleadoMaxPiezas(piezasProducidasEmpleados)
    EntregarPremio(idMax)

    for i in 1..E {
        V(seEntregoPremio)
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/57b27eb2-23be-411a-a232-b7cefec347fc)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/28d7362a-3b67-4325-99e7-791409893d32)


![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/0618ea46-8fac-42d8-9f90-a7aeb44bd148)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/4c146bf3-1ad5-44f3-96b4-f94476491233)