```java
procedure basquet
    task type Jugador;
        entry terminoPartido();
    end
    arrJugadores: (1..20) of Jugador;

    task body Jugador is
    begin 
        Entrenador.cancha(idCancha)
        Cancha[idCancha].jugar()
        Entrenador.terminoPartido();
    end body;


    task Entrenador is:
        entry cancha(idCancha:OUT Integer);
    end Entrenador;

    task body Entrenador is
        num:Integer:=1;
    begin
        for i in 1..22 loop
            select:
                accept cancha(idCancha:OUT Integer) do
                    idCancha:=num;
                end cancha;
                num:=3-num; // toggle
            or:
                accept terminoCancha();
        end loop;
        Charla() // hace delay de 10 mins
        for i in 1..20 loop
            accept terminoPartido();
        end loop;
    end body;

    task type Cancha is:
        entry jugar();
    end
    arrCanchas: (1..2) of Cancha;

    task body Cancha is
    begin
        for i in 1..10 loop
            accept jugar()
        end loop;
        delay 40*60; // juegan
        Entrenador.terminoCancha()
    end body;

begin

end basquet;
```
