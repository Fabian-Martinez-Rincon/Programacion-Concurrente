```java
process Empleado[]{
    Buffer!siguiente()
    Persona[*]?termino()
}
process Persona[id:0..P-1]{
    Buffer!llegue(id)
    Buffer[id]?usar()
    UsarSimulador()
    Empleado!termino()
}

process Buffer[]{
    do Persona[*]?llegue(idPers) => push(colaPers,idPers)
    [] not empty(colaPers); Empleado?siguiente() => Persona[pop(colaPers)]!usar()
    od
}
```

# o con passing the baton/condition ish

```java
process Empleado[]{
    libre=true
    do libre;Persona[*]?llegue(idPers)=>libre=false;Persona[idPers]!usar()
    [] not libre;Persona[*]?llegue(idPers) => push(colaPers,idPers)
    [] empty(colaPers);Persona[*]?termino() => libre=true;
    [] not empty(colaPers);Persona[*]?termino() => Persona[pop(colaPers)]!usar()
    od

}
process Persona[id:0..P-1]{
    Empleado!llegue(id)
    Empleado[id]?usar()
    UsarSimulador()
    Empleado!termino()
}
```
