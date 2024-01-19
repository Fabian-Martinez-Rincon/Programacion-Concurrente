```java
procedure ej3
    task type Servidor is
        entry checkear(sec:IN text; idCli:IN Integer);
    end Servidor;
    arrServidor:array 1..5 of Servidor;

    task body Servidor is
        idCli:Integer:=-1;
        secuencia,res:text:="";
    begin
        Buffer.listo(idCliente,secuencia);
        res:=ResolverAnalisis(secuencia);
        Cliente[idCliente].resultado(res);
    end body

    task type Cliente is:
        entry resultado(res:IN text);
    end Cliente;
    arrCliente:array 1..N of Cliente;

    task body Cliente is
        id:Integer:=-1;
    begin
        accept ident(idCli:IN Integer) do
            id:=idCli;
        end ident;
        loop 
            sec=GenerarSecuencia();
            Buffer.pedido(sec,id);
            accept resultado(res:IN text);
        end loop;
    end body;

    task Buffer is:
        entry listo(idServ:IN Integer; idCliente:OUT Integer; secuen:OUT text);
        entry pedido(sec:IN text; id:IN Integer);
    end Buffer;

    task body Buffer is
    begin
        loop
            accept listo(idCliente:OUT Integer; secuen:OUT text) do
                accept pedido(sec:IN text; idCli:IN Integer) do
                    idCliente:=idCli;
                    secuen:=sec;
                end checkear;
            end listo;
        end loop;
    end body;

begin
    for j in 1..N loop
        Cliente[i].ident(i)
    end loop;
    for i in 1..5 loop
        Servidor[i].ident(i);
    end loop;
end ej3;
```
