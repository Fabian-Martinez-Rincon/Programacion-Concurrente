```java
chan siguiente(int);
chan atencion(int,text);
chan solicitud[3](int,text);
chan resultado[P](text);

process Persona[id:0..P-1]{
    send atencion(id,tramite);
    receive resultado[id](res);
}
process Buffer[]{
    while(true){
        receive siguiente(idEmp);
        if (!empty(atencion)){
            receive atencion(idPers,tramite);
        }else{
            idPers=-1;
            tramite="";
        }
        send solicitud[idEmp](idPers,tramite);
    }
}
process Empleado[id:0..2]{
    while(true){
        send siguiente(id);
        receive solicitud[id](idPers,tramite);
        if (id==-1){
            delay(5);
        }else{
            res=ResolverTramite(tramite);
            send resultado[idPers](res);
        }
    }
}
```
