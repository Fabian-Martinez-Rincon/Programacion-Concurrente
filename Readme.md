

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



![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/c652f033-140d-4089-b978-9dd435494cdd)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/956cf904-ec12-4e4f-8051-d8efbf8fc5fe)