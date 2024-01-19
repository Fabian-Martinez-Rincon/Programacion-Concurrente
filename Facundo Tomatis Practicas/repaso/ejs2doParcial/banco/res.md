```java
procedure ej1;
    task type Persona
    end Persona;
    
    arrPersonas: (1..N) of Persona;
    
    task body Persona is
    begin
        select
            if (ObtenerTipo()=="jubilado") then
                Banco.colaJubilado();
            else 
                Banco.colaNormal();
            end if;
        or delay 15min
            Informes.nota(nota);
        end select;
    end body;

    task body Banco is
    begin
        loop
            select
                accept colaJubilado() do
                    // atender
                end colaJubilado;
            or when(colaJubilado'count=0) =>
                accept colaNormal() do
                    // atender
                end colaNormal;
            end select;
        end loop;

    end body;

    task body Informes is
        reclamos:Queue;
    begin
        accept nota(nota:IN text) do
            push(reclamos,nota);
        end nota;
    end body;
begin

end ej1;
```
# al profe no le gustan los ifs dentro del select
```java
procedure ej1;
    task type Persona
    end Persona;
    
    arrPersonas: (1..N) of Persona;
    
    task body Persona is
    begin
        if (ObtenerTipo()=="jubilado") then
            select
                Banco.colaJubilado();
            or delay 15min
                Informes.nota(nota);
            end select;
        else 
            select
                Banco.colaNormal();
            or delay 15min
                Informes.nota(nota);
            end select;
        end if;
    end body;

    task body Banco is
    begin
        loop
            select
                accept colaJubilado() do
                    // atender
                end colaJubilado;
            or when(colaJubilado'count=0) =>
                accept colaNormal() do
                    // atender
                end colaNormal;
            end select;
        end loop;

    end body;

    task body Informes is
        reclamos:Queue;
    begin
        accept nota(nota:IN text) do
            push(reclamos,nota);
        end nota;
    end body;
begin

end ej1;
```
