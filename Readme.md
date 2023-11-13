

<div align="center"> 

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&duration=1200&pause=1000&color=F78E23&center=true&width=435&lines=Programación Concurrente"/>

</div>


<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%">



- [Explicaciones Teoricas](https://youtube.com/playlist?list=PLH8A0IjFldaGLATsgRdmPBtiNcp5KmAHo)
- [✅ Practica 1 Variables Compartidas](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica1.html)
- [✅ Practica 2 Semáforos](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica2.html)
- [✅ Practica 3 Monitores](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica3.html)

### Practica 4 Pasaje de Mensajes Asincronico (PMA)

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

```c

send canalUsuario(text)

proces Usuarios[id:0..n-1]{
    text documento

    while (true){
        documento = generarDocumento()
        send canalUsuario(documento)
    }
}

chan canalDirector(text)

process Director {
    text documento
    while (true){
        documento = generarDocumento()
        send canalDirector(documento)
    }
}


chan canalImpresora(int)
chan imprimir[3](text)

proces Impresora[id:0..2]{
    text documento
    while(true){
        send canalImpresora(id)
        receive imprimir[id](documento)
        imprimirDocumento(docuemtno)
    }
}

process Coordinador(){
    int idIpresora
    text documento
    while (true){
        receive canalImpresora(idImpresora)

        if (not empty(canalDirector)){
            receive canalDirector(documento)
        }
        else{
            receive canalUsuario(documento)
        }
        send imprimir[idImpresora](documento)
    }
}
```

### Practica 4 Pasaje de Mensajes Sincronico (PMS)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/1478c416-cec2-4a08-b9ab-704a75c33f34)
![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/746301be-7c5a-427b-996e-40f71bc5c5d5)

```c
process Examinador[id:0..R-1]{
    texto direccion
    while (true){
        direccion = BuscarSitioInfectado()
        admin!etiquetaExaminador(direccion)
    }
}

process Analizador{
    texto direccion
    text resultado
    while (true){
        Admin!etiquetaAnalizador()
        Admin?etiquetaExaminador(direccion)
        resultado = examinarSitio(direccion)
    }
}

process Admin{
    text direccion
    Cola sitiosEspera
    text elemento
    do
        Examinador[*]?etiquetaExaminador(direccion) --> sitiosEspera.push(direccion)
        [] not empty (sitiosEspera); Analizador?etiquetaAnalizador()
            --> 
                elemento = pop(sitiosEspera)
                Analizador!etiquetaExaminador(elemento)
    od
}

```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/75d6815d-3e46-4fc2-b416-4a4772a4fa48)

```c
process PrimerEmpleado{
    text muestra
    while (true){
        muestra = prepararMuestra()
        Admin!muestrasGeneradas(muestra)
    }
}

process Admin{
    cola muestrasEspera
    text muestraActual

    do PrimerEmpleado?muestrasGeneradas(muestraActual) --> muestrasEspera.push(muestraActual)
    [] not empty(muestrasEspera); SegundoEmpleado?estoySegundoEmpleado() -->
        muestraActual = muestrasEspera.pop()
        SegundoEmpleado!muestrasGeneradas(muestraActual) 
    od
}


process SegundoEmpleado{
    texto muestra
    texto resultado
    while (true){
        Admin!estoySegundoEmpleado()
        Admin?muestrasGeneradas(muestra)

        muestra = ArmarSetAnalisis(muestra)

        TercerEmpleado!muestraArmada(muestra)
        TercerEmpleado?muestraAnalizada(resultado)

        archivar(resultado)
    }
}

process TercerEmpleado{
    texto muestra
    texto analizada
    while (true){
        SegundoEmpleado?muestraArmada(muestra)
        analizada = analizarMuestra(muestra)
        SegundoEmpleado!muestraAnalizada(analizada)
    }
}


```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/1aa733fd-04d6-4885-ab70-6560b961bbaa)

#### Punto A

```c
process Alumno[id:0..n-1]{
    text examen
    int nota

    examen = Resolver(examen)
    Profesor!examenTerminado(examen)
    Profesor?examenCorregido(nota)
}

process Profesor{
    text examen
    int nota

    while (true){
        Alumno?examenTerminado(examen)
        nota = corregir(examen)
        Alumno!examenCorregido(nota)
    }
}
```

#### Punto B

```c
process Alumno[id:0..n-1]{
    text examen
    int nota

    examen = Resolver(examen)
    Admin!examenTerminado(id, examen)
    Profesor[*]?examenCorregido(nota)
}

process Admin{
    text examen
    int idAlumno
    int idProfesor
    cola examenesResueltos

    do Alumno[*]?examenTerminado(idAlumno, examen) --> examenesResueltos.push(idAlumno, examen)
    [] not empty(examenesResueltos); Profesor[*]?estoyProfe(idProfesor) -->
        idAlumno, examen = pop(examenesResueltos)
        Profesor[idProfesor]!(idAlumno, examen)
    od
}

process Profesor[id:0..p-1]{
    text examen
    int nota
    int idAlumno
    while (true){
        Admin!estoyProfe(id)
        admin?examenTerminado(idAlumno, examen)
        nota = corregir(examen)
        Alumno[idAlumno]!examenCorregido(nota)
    }
}
```

#### Punto C

```c
process Alumno[id:0..n-1]{
    text examen
    int nota

    Admin!llegoAlumno()
    Admin?comenzarAlumno()
    examen = Resolver(examen)
    Admin!examenTerminado(id, examen)
    Profesor[*]?examenCorregido(nota)
}

process Admin{
    text examen
    int idAlumno
    int idProfesor
    cola examenesResueltos

    for (i=0; i<N; i++){
        Alumno[*]?llegoAlumno()
    }
    for (i=0; i<N; i++){
        Alumno[*]!comenzarAlumno()
    }

    do Alumno[*]?examenTerminado(idAlumno, examen) --> examenesResueltos.push(idAlumno, examen)
    [] not empty(examenesResueltos); Profesor[*]?estoyProfe(idProfesor) -->
        idAlumno, examen = pop(examenesResueltos)
        Profesor[idProfesor]!(idAlumno, examen)
    od
}

process Profesor[id:0..p-1]{
    text examen
    int nota
    int idAlumno
    while (true){
        Admin!estoyProfe(id)
        admin?examenTerminado(idAlumno, examen)
        nota = corregir(examen)
        Alumno[idAlumno]!examenCorregido(nota)
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/719e3c10-db7d-455e-904a-ddf697a76387)

```c
process Persona[id:0..p-1]{
    text tiempoAcceso

    Admin!llegoPersona(id)
    Encargado?turnoPersona(tiempoAcceso)

    UsarSimulador(tiempoAcceso)
    Encargado!terminoPersona()
}
process Admin{
    int idPersona
    cola personasLlegada

    do Persona[*]?llegoPersona(idPersona) --> personasLlegada.push(idPersona)
    []  not empty(personasLlegada); Encargado?estoyEncargado() -->
            idPersona = pop(personasLlegada)
            Encargado!recibirPersona(idPersona)
    od
}
process Encargado{
    int idPersona
    text tiempoAcceso
    while (true) {
        Admin!estoyEncargado()
        Admin?recibirPersona(idPersona)
        tiempoAcceso = calcularTiempo(idPersona)
        Persona[idPersona]!turnoPersona(tiempoAcceso)
        Persona[idPersona]?terminoPersona()
    }
}
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/90d4dc64-099e-455e-8524-fc5bdaa3aed2)

```c
process Espectador[id:0..p-1]{
    text tiempoAcceso

    Admin!llegoEspectador(id)
    Turno?turnoEspectador(tiempoAcceso)

    UsarMaquina(tiempoAcceso)
    Turno!terminoEspectador()
}
process Admin{
    int idEspectador
    cola espectadorLlegada

    do Espectador[*]?llegoEspectador(idEspectador) --> espectadorLlegada.push(idEspectador)
    []  not empty(espectadorLlegada); Turno?estoyTurno() -->
            idEspectador = pop(espectadorLlegada)
            Turno!recibirPersona(idEspectador)
    od
}
process Turno{
    int idEspectador
    text tiempoAcceso
    while (true) {
        Admin!estoyTurno()
        Admin?recibirPersona(idEspectador)
        tiempoAcceso = calcularTiempo(idEspectador)
        Persona[idEspectador]!turnoPersona(tiempoAcceso)
        Persona[idEspectador]?terminoPersona()
    }
}
```

### Practica 5 Ada

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/44f0327f-a48b-4845-9d57-3c6f819c2ec6)

#### Parte a

```Ada
Procedure ejercicio1 is
Task Puente is
    entry INGRESO_AUTO;
    entry INGRESO_CAMIONETA;
    entry INGRESO_CAMION;
    entry SALIR_AUTO;
    entry SALIR_CAMIONETA;
    entry SALIR_CAMION;
END puente;

Task type vehiculo

arrAuto: array (1..A) of vehiculo;
arrCamioneta: array (1..A) of vehiculo;
arrCamion: array (1..A) of vehiculo;

Task body vehiculo  is
begin
    if ("Auto") then
        Puente.INGRESO_AUTO;
    else if ("Camioneta") then
        Puente.INGRESO_CAMIONETA;
    else if ("Camion") then
        Puente.INGRESO_CAMION;
    
    if("Auto")then
        Puente.SALIR_AUTO;
    else if("Camioneta")then
        Puente.SALIR_CAMIONETA;
    else 
        Puente.SALIR_CAMION;
end vehiculo;

Task Body Puente is
    pesoActual:int = 0
begin
    SELECT
        WHEN (pesoActual + 1 <= 5) => ACCEPT INGRESO_AUTO
    OR
        WHEN (pesoActual + 2 <= 5) => ACCEPT INGRESO_CAMIONETA
    OR
        WHEN (pesoActual + 3 <= 5) => ACCEPT INGRESO_CAMION
    OR
        ACCEPT SALIR _AUTO;
        pesoActual -= 1;
    OR
        ACCEPT SALIR_CAMIONETA;
        pesoActual -= 2;
    OR
        ACCEPT SALIR_CAMION;
        pesoActual -= 3;
    END SELECT
end Puente;


begin
    null
end ejercicio1
```

#### Parte b

```Ada
Procedure ejercicio1 is
Task Puente is
    entry INGRESO_AUTO;
    entry INGRESO_CAMIONETA;
    entry INGRESO_CAMION;
    entry SALIR_AUTO;
    entry SALIR_CAMIONETA;
    entry SALIR_CAMION;
END puente;

Task type vehiculo

arrAuto: array (1..A) of vehiculo;
arrCamioneta: array (1..A) of vehiculo;
arrCamion: array (1..A) of vehiculo;

Task body vehiculo  is
begin
    if ("Auto") then
        Puente.INGRESO_AUTO;
    else if ("Camioneta") then
        Puente.INGRESO_CAMIONETA;
    else if ("Camion") then
        Puente.INGRESO_CAMION;
    
    if("Auto")then
        Puente.SALIR_AUTO;
    else if("Camioneta")then
        Puente.SALIR_CAMIONETA;
    else 
        Puente.SALIR_CAMION;
end vehiculo;

Task Body Puente is
    pesoActual:int = 0
begin
    SELECT
        WHEN (pesoActual + 1 <= 5) and (INGRESO_CAMION`COUNT = 0) => ACCEPT INGRESO_AUTO
    OR
        WHEN (pesoActual + 2 <= 5) and (INGRESO_CAMION`COUNT = 0) => ACCEPT INGRESO_CAMIONETA
    OR
        WHEN (pesoActual + 3 <= 5) => ACCEPT INGRESO_CAMION
    OR
        ACCEPT SALIR _AUTO;
        pesoActual -= 1;
    OR
        ACCEPT SALIR_CAMIONETA;
        pesoActual -= 2;
    OR
        ACCEPT SALIR_CAMION;
        pesoActual -= 3;
    END SELECT
end Puente;


begin
    null
end ejercicio1
```

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/5ff92cf2-679b-446a-af95-ddb778516e87)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/91941f1c-23f1-4cdb-a080-3f6df2169072)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/62953c79-ea95-497c-a861-8af7a5d4bac2)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/9391225b-535f-45e6-aff6-0d720be5e24e) ![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/03e526a8-3124-432e-b59f-8d523ce31ae8)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/d3c6bc57-98a7-4751-b429-8064183e04e9)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/d97a2f32-6cfd-44c0-a410-ad79214d1d19)

![image](https://github.com/Fabian-Martinez-Rincon/Fabian-Martinez-Rincon/assets/55964635/678917b0-d226-4574-ad38-62a5813e00f2)