# Mio
```java
process Empleado[id:0..4]{
    while (true){
        send siguiente(id);
        receive enviarListado[id](idPers,listado)
        presupuesto=HacerPresupuesto(listado);
        send resultado[idPers](presupuesto)
    }
}
process Persona[id:0..N-1]{
    send llegue(id);
    receive respuesta[id](idEmp);
    send enviarListado[idEmp](id,listado);
    receive resultado[id](presupuesto);

}
process Buffer[]{
    while(true){
        receive siguiente(idEmp)
        receive llegue(idPers)
        send respuesta[idPers](idEmp)
    }
}

```

# Profe
```java
process Empleado[id:0..4]{
    while (true){
        receive llegue(idPers)
        send respuesta[idPers](id)
        receive enviarListado[id](listado)
        presupuesto=HacerPresupuesto(listado);
        send resultado[idPers](presupuesto)
    }
}
process Persona[id:0..N-1]{
    send llegue(id);
    receive respuesta[id](idEmp);
    send enviarListado[idEmp](id,listado);
    receive resultado[id](presupuesto);

}

```
