```java
procedure ejSitio
    N:=I+P;

    task type Paciente;
    arrPaciente: (1..P) of Paciente;

    task body Paciente is
        atendio:Boolean:=false;
    begin 
        while (not atendio) loop
            select 
                Servidor.comprar(vendio);
                atendio:=true;
            or delay(5*60)
                null;
            end select;
        end loop;
    end body;

    task type Impaciente;
    arrImpaciente: (1..I) of Impaciente;

    task body Impaciente is
        atendio:Boolean:=false;
    begin 
        while (not atendio) loop
            select 
                Servidor.comprar(vendio);
                atendio:=true;
            else
               delay 10;
            end select;
        end loop;
    end body;

    task Servidor is:
        entry comprar(vendio:OUT Boolean);
    end Servidor;

    task body Servidor is
        cantVendida:Integer:=0;
    begin
        loop
            accept comprar(vendio:OUT Boolean) do
                if (cantVendida==E){
                    vendio:=false;
                }else{
                    cantVendida:=cantVendida+1;
                    vendio:=true;
                }
            end comprarPaciente;
        end loop;
    end body;
begin
    null;
end ejSitio;
```
