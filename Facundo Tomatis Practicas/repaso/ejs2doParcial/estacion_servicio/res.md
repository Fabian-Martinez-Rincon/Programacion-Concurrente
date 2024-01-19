```java
process Empleado{
    for (int i=0;i<N;i++){
        Buffer!listo();
        Buffer?proximo(idCli);
        Cliente[idCli]!atencion()
        Cliente[idCli]?cargar(tipo,cuanto)
        cargarCombustible(tipo,cuanto)
        Cliente[idCli]!termino();
    }
}

process Cliente[id:0..N-1]{
    Buffer!llegue(id);
    Empleado?atencion();
    Empleado!cargar(tipo,cuanto);
    Empleado?termino();
}

process Buffer[]{
    do Cliente[*]?llegue(idCli) => push(colaCli,idCli);
    [] not empty(colaCli);Empleado?siguiente() => 
        Empleado!proximo(pop(colaCli));
}
```
