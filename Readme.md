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
text contenedores[P]
sem cantidad = P


process Preparador{
    Paquete p
    while (true){
        Preparar(p)


    }
}
process Entregador{

}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/156e9ed9-4b87-4c93-82f9-311dcd3bea05)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/9d705b69-2c45-48fc-800f-9b1db7bc30e3)
![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/5dd12e19-1bcb-4bd1-803d-1eca76c13cb0)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/90f8ff11-9b18-4e22-be3c-a9eb1ab73c35)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/57b27eb2-23be-411a-a232-b7cefec347fc)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/28d7362a-3b67-4325-99e7-791409893d32)


![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/0618ea46-8fac-42d8-9f90-a7aeb44bd148)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/4c146bf3-1ad5-44f3-96b4-f94476491233)