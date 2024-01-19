```java
process Programador[id:0..2]{
    while(true){
        send siguiente(id);
        send sync
        receive respuesta[id](reporte);
        if (reporte==""){
            Programar()
        }else{
            ResolverError(reporte)
        }
    }
}

process Cliente[id:0..N-1]{
    while (true){
        send reporte(error)
        send sync
    }
}

process Buffer[]{
    while (true){
        receive sync
        if (not empty(atencion)){
            receive siguiente(idPr);
            if (empty(reportes)){
                send respuesta[idPr]("");
            } else{
                send respuesta[idPr](pop(reportes))
            }
        }else{
            receive reporte(error)
            push(reportes,eror)
        }
    }
}
```

# otra
```java
process Programador[id:0..2]{
    while(true){
        send siguiente(id);
        receive respuesta[id](reporte);
        if (reporte==""){
            Programar()
        }else{
            ResolverError(reporte)
        }
    }
}

process Cliente[id:0..N-1]{
    while (true){
        send reporte(error)
    }
}

process Buffer[]{
    receive siguiente(idPr);
    if (empty(reporte)){
        error=""
    } else{
        receive reporte(error)
    }
    send respuesta[idPr](error)
}
```
