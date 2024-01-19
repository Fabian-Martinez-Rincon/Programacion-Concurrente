```java
procedure ej3
    task Empleado is:
        entry pedidoAnciano();
        entry pedidoEmbarazada();
        entry pedidoRegular();
    end Empleado;
    task body Empleado is
    begin
        loop
            select
                accept pedidoEmbarazada() do
                    AtenderPedido();
                end pedidoEmbarazada;
            or when(pedidoEmbarazada'count=0)=>
                accept pedidoAnciano() do
                    AtenderPedido();
                end pedidoAnciano;
            or when(pedidoEmbarazada'count=0 and pedidoAnciano'count=0)=>
                accept pedidoRegular() do
                    AtenderPedido();
                end pedidoRegular
            end select;
        end loop;
    end body;


    N:=A+E+R;
    task type Anciano;
    arrAncianos:array 1..A of Anciano;
    task body Anciano is
    begin
        select
            Empleado.pedidoAnciano();
        or delay 5*60
            null;
        end select;
    end body;

    task type Embarazada;
    arrEmbarazadas:array 1..E of Embarazada;
    task body Embarazada is
    begin
        select
            Empleado.pedidoEmbarazada();
        else
            null;
        end select;
    end body;

    task type Regular;
    arrRegulares:array 1..R of Regular;
    task body Regular is
    begin 
        Empleado.pedidoRegular();
    end body;
begin

end ej3;
```
