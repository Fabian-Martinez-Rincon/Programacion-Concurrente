```haskell
process Corredor[id:0..C-1]{
    Buffer!llegar(id);
    Coordinador[*]?(numChaleco)
}
```

```java
process Coordinador[id:0..2]{
    while(true){
        Buffer!listo(id);
        Buffer?proximo(idCorredor);
        Corredor[idCorredor](ObtenerChaleco());
    }
}
```

```java
process Buffer[]{
    do Corredor[*]?llegar(idCorr) => push(colaEspera,idCorr);
    [] !empty(colaEspera);Coordinador[*]?listo(idCoord) => 
        Coordinador[idCoord]!proximo(pop(colaEspera))
    od
}
```
