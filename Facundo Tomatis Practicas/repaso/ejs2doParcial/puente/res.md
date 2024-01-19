```java
procedure ejPuente
    task type Persona;

    arrPers: (1..N) of Persona;

    task body Persona is
    begin;
        if (SoyJubilado()){
            Puente.entrarJubilado();
        }else{
            Puente.entrar();
        }
        // usar
        Puente.salir();
    end body;

// ---------------------------------------------

    task Puente is:
        entry salir();
        entry entrar();
        entry entrarJubilado();
    end Puente;

    task body Puente is
        cantidad:Integer:=100;
    begin
        loop
            select:
                accept salir();
                cantidad:=cantidad+1;
            or: when(cantidad>0)=>
                accept entrarJubilado();
                cantidad:=cantidad-1;
            or: when(cantidad>0 and entrarJubilado'count=0)=>
                accept entrar();
                cantidad:=cantidad-1;
            end select;
        end loop;
    end body;
begin
    null;
end ejPuente;
```

