

<div align="center"> 

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&duration=1200&pause=1000&color=F78E23&center=true&width=435&lines=Programación Concurrente"/>

</div>


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">



- [Explicaciones Teoricas](https://youtube.com/playlist?list=PLH8A0IjFldaGLATsgRdmPBtiNcp5KmAHo)
- [✅ Practica 1 Variables Compartidas](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica1.html)
- [✅ Practica 2 Semáforos](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica2.html)
- [✅ Practica 3 Monitores](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica3.html)

#### Practica 4 Pasaje de Mensajes Asincronico (PMA)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/79d4a6a1-2da8-4575-b7b8-7372393c68e0)

**Punto a)**

```c
chan canalCliente(int)
chan antendido[n]()

process Cliente [id:0..n-1]{
    send canalCliente(id)
    receive atendido[id]()
}

process Empleado {
    while (true){
        receibe canalCliente(id)
        //Atender Empleado
        send atendido[id]()
    }
}
```

**Punto b)**

```c
chan canalCliente(int)
chan antendido[n]()

process Cliente [id:0..n-1]{
    send canalCliente(id)
    receive atendido[id]()
}

process Empleado [id: 0..1] {
    while (true){
        receibe canalCliente(id)
        //Atender Empleado
        send atendido[id]()
    }
}
```

**Punto c)**

```c
chan canalCliente(int)
chan antendido[n]()

chan canalEmpleado(int)
chan siguiente[2](int)


process Cliente [id:0..n-1]{
    send canalCliente(id)
    receive atendido[id]()
}

process Administrador {
    int idC
    int idE
    while (true){
        receive canalEmpleado(idE)
        if (not empty(canalCliente)){
            receive canalCliente(idC)
        }
        else{
            idC := -1
        }
        send siguiente[idE](idC)
    }
}

process Empleado [id: 0..1] {
    int idC
    while (true){
        send canalEmpleado(id)
        receive siguiente[id](idC)
        if (idC <> -1){
            //Antender Cliente
            send antendido[idC]()
        }
        else {
            delay(15 minutos)
        }
        
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/980762e9-0f58-42e1-bf11-03bf2bfffbea)


```c
chan canalCliente(int)
chan canalClienteTermino(int)
chan hayPedido()

chan colaMasCorta[p](int)
chan canalComprobante[p](text)

chan canalCaja[5](int)



process Cliente [id: 0..p-1]{

    int idCajero

    send canalCliente(id)
    send hayPedido()

    //Espero recibir la fila mas corta
    receive colaMasCorta[id](idCajero) 
    UsarCajero(idCajero)

    send canalCaja[idCajero](id) //Aviso para que me den el comprobante
    receive canalComprobante[id](comprobante)

    send canalClienteTermino(idCajero)

}

process Cajero [id: 0..4] {
    int idCliente
    text comprobante

    while (true){
        receive canalCaja[id](idCliente)
        generarComprobanmte(idCliente)
        send canalComprobante[idCliente](comprobante)
    }
}

process Coordinado{
    int idCliente
    int idCajero
    Array cajasCantidad[5]=[5](0)
    int menorFila

    while (true){
        receive hayPedido()
        if(not empty(canalClienteTermino)){
            receive canalClienteTermino(idCajero)
            cajasCantidad[idCajero]--
        }
        else if(not empty(canalCliente)){
            receive canalCliente(idCliente)
            idMenorFila = min(cajasCantidad)
            
            send colaMasCorta[idCliente](idMenorFila)
            cajasCantidad[idMenorFila]++
        }
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/d2c0f1b2-ed53-4006-a840-6f9832c47102)

Cuando nos dicen que son tomados por cualquiera quiere decir que necesitamos un canal para ese proceso y que nos indique cual es el siguiente, y tambien tenemos un proceso coordinador cada vez que tengo que hacer algo si un canal esta vacio

```c
chan canalCliente(int,text)
chan canalPlatosListo[C](text)

process Cliente [id:0..C-1]{
    text plato

    send canalCliente(id,plato)
    receive canalPlatoListo[id](plato)
}

chan canalVendedor(int)
chan vendedorSiguiente[3](text)

chan canalPlatosEspera(text)

process Vendedor[id:0..2]{
    int idCliente
    text Plato
    while (true){
        send canalVendedor(id)
        receive vendedorSiguiente[id](idCliente, Plato)

        if (Plato == "vacio"){
            reponerPackBebidas()
            delayRange(60-180)
        }
        else{
            send canalPlatosEspera(idCliente, Plato)
        }
    }
}

process Coordinador{
    int idVendedor
    int idCliente
    text Plato
    while (true){
        receive canalVendedor(idVendedor)

        if (empty(canalCliente)){
            Plato := 'vacio'
        }
        else{
            receive canalCliente(idCliente, Plato)
        }
        send vendedorSiguiente[idVendedor](idCliente, Plato)
    }
}

process Cocinero(){
    text Plato
    int idCliente
    while(true){
        receive canalPlatosEspera(idCliente, Plato)

        cocinarPlato(Plato)
        send canalPlatosListo[idCliente](Plato)
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/c652f033-140d-4089-b978-9dd435494cdd)

En este ejercicio ocurre algo que en los demas no, y es que no tenemos un procesos coordinador, en este caso lo que necesitamos es un semaforo para sincronizacion

```c
chan canalCliente(int)
chan cabinaIr[N]()

chan usarCabina(int)
chan esperandoTicket[N](text)

chan hayPedido()//Canal Solo para Sincronizacion

process Cliente []{
    int cabinaCorta
    text dinero
    text ticket

    send canalCliente(id)
    
    //Solicitamos al empleado para una cabina
    hayPedido()
    receive cabinaIr[id](cabinaCorta)
    usarCabina(cabinaCorta)

    //Solicitamos al empleado para pagar
    hayPedido()
    send pagarEmpleado(id, dinero, cabinaCorta)

    receive esperandoTicket[id](ticket)
}

process Empleado{
    Arreglo cabinas[10] = [10,0]
    int cabinaChica
    int idCliente
    text Ticket

    while (true){
        //Podemos tener dos casos de pedidos
        receive hayPedido() 
        // Si tengo las cabinas llenas tengo que preguntar
        // Asi espero a que la gente termine
        if (not empty(pagarEmpleado)) || (cabinas.todasOcupadas()){
            receive pagarEmpleado(idCliente, dinero, cabinaChica)
            cabinas.push(cabinaChica)//Vuelvo a agregar la cabina usada
            Ticket = Cobrar(idCliente,dinero)
            
            send esperandoTicket[idCliente](Ticket)
        }
        else{
            receive canalCliente(idCliente)
            cabinaChica = cabinas.popChica()
            send cabinaIr[idCliente](cabinaChica)
        }            

    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/956cf904-ec12-4e4f-8051-d8efbf8fc5fe)