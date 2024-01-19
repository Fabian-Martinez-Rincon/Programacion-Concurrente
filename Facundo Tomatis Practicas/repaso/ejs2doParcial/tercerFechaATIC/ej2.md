```java
process Turista[id:0..19]{
    Empleado!llegue()
    Empleado?terminoCharla()
    Guia!permiso(id)
    Guia?puedo()
    UsarTirolesa()
    Guia!libre()
}

process Empleado{
    for i in 1..20{
        Turista[*]?llegue();
    }
    DarCharla();
    for i in 0..19{
        Turista[i]!terminoCharla();
    }
}

process Guia{
    for i in 1..20{
        if 
        [] libre Turista[*]?permiso(id) => 
            libre=false; Turista[id]!puedo();
        [] not libre Turista[*]?permiso(id) => 
            push(pendientes,id);
        [] empty(pedidos) Turista[*]?libre() => 
            libre=true;
        [] !empty(pedidos) Turista[*]?libre() => 
            Turista[pop(pendientes)]!puedo();
        fi
    }
}
```
