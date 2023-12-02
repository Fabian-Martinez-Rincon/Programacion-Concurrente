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
- Siempre que indique algun tipo de orden de llegada, vamos a usar una cola. Cada vez que hagamos una operacion de push y pop sobre esa cola, vamos a usar Mutex