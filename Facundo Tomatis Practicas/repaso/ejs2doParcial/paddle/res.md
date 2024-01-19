```java
procedure ejPaddle is

    task type Cancha is:
        entry jugar();
        entry terminoPartido();
    end Cancha;
    arrCanchas:array 1..10 of Cancha;

    task body Cancha is
    begin
        for i in 1..4 loop
            accept jugar();
        end loop;
        delay(60*60) // juegan
        for i in 1..4 loop
            accept terminoPartido();
        end loop;
    end body;

    task Encargado is:
        entry cancha(idCancha:OUT Integer);
    end Encargado;

    task body Encargado is
    begin
        for i in 1..40 loop
            accept cancha(idCancha:OUT Integer) do
                idCancha:=(i-1)/4+1;
            end cancha;
        end loop;
    end body;

    task type Persona;
    arrPersona:array 1..40 of Persona;

    task body Persona is
        idCancha:Integer:=-1;
        id:Integer:=-1;
    begin
        Encargado.cancha(idCancha)
        Cancha[idCancha].jugar(id)
        Cancha[idCancha].terminoPartido()
    end
begin

end ejPaddle;
```
