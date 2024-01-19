```java
procedure recursosHumanos
    task Directora is:
        entry llegue(datos:IN text);
        entry examen(examen:OUT text);
        entry corregir(res:IN text,califacion:OUT Integer);
    end Directora;

    task body Directora is
        exam:text:="...";
    begin
        for i in 1..20 loop:
            accept llegue(datos:IN text) do
                Registar_Persona(datos);
            end llegue;
        end loop;
        for i in 1..20 loop:
            accept examen(exame:OUT text) do
                exame:=exam;
            end llegue;
        end loop;
        for i in 1..20 loop:
            accept corregir(res:IN text, califacion:OUT Integer) do
                califacion:=Corregir_Examen(res);
            end llegue;
        end loop;
    end body;
    
    task type Persona;
    arrayPers:array 1..20 of Persona;
    
    task body Persona is
        examen,res,datosPersonales:text:="...";
        calificacion:Integer:=-1;
    begin
        Directora.llegue(datosPersonales);
        Directora.examen(examen);
        res:=Resolver_Examen(examen);
        Directora.corregir(res,calificacion);
    end body;

begin

end recursosHumanos;
```
