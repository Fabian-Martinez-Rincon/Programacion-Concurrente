# Introduccion Memoria Distribuida
mecanismo de comunicacion/sincronizacion => intercambio de mensajes

## Programa Distribuido
Programa concurrente que utiliza pasaje de mensajes para comunicarse. Supone que la arquitectura es distribuida

## Canales
### Tipos
- Mailbox (todos pueden acceder)
- input port (muchos pueden mandar pero solo uno puede recibir)
- link (uno solo puede enviar y uno solo puede recibir)
### Direccion
- Unidireccionales (envian informacion por un canal)
- Bidireccionales (envian y reciben informacion por el mismo canal)
### Sincronismo
- Sincronicos (espera a que el proceso receptor lo reciba)
- Asincronicos (NO espera a que el proceso receptor lo reciba)
 

## Relacion entre mecanismos de sincronizacion
```text
                             .-> Monitores -> RPC
                            /                  ∧
Busy waiting -> Semaforos --                   |
                            \                  ∨
                             .-> PM(A/S) -> Rendezvous
```
- Semaforos: Mejora de busy waiting, mas simple
- Monitores: combinan exclusion mutua implicita y señalizacion explicita (mas abstracto)
- PMA/S: extiende semaforos con datos V=send, P=receive
- RPC: "monitores" en difs maquinas a traves de mensajes, bidireccional
- Rendezvous: similar a PMS pero con canales Bidireccionales

---

# PMA
colas con mensajes enviados y aun no recibidos
mailbox, unidireccional, asincronicos
```haskell
chan nombreCanal(tipo1,tipo2,tipoN); -- declaracion
send nombreCanal(expr1,expr2,exprN); -- no bloqueante, cola ilimitada, inst atomica
receive nombreCanal(var1,var2,varN); -- bloqueante hasta que haya, toma el primero
empty(nombreCanal) -- devuelve true si no hay mensajes, si no false
```
posible interferencia entre medio de dos instrucciones atomicas
se puede usar mailbox para que funcionen como input port o link

---

## Filtro
recibe mensajes de n canales, envia a n canales. modifica la informacion recibida dependiendo de su estado y valores recibidos

---

## Clientes y Servidores
### Servidor
recibe mensajes de clientes, resuelve y devuelve al cliente en particular
### Cliente
envia mensaje a canal de requerimientos general (tmb manda id), recibe en su propio canal

### Monitor (simularlo)
manejar recurso compartido a traves de proceso servidor y pasaje de mensajes

Diferentes problemas:
- multiples operaciones (receive con op y hacer un case)
- multiples operaciones y variables condicion (receive con op y si no puede encolar el pedido)
- sentencia de alternativa multiple (con if no deterministico)
- continuidad conversacional (send por global, receive por propio y send a especifico)
 
---

## Pares interactuantes

### Modelos arquitecturales
- Centralizada (procesos se comunican con uno central y solamente con ese)
Nro lineal de mensajes los mensajes al central gralmente se hacen al mismo tiempo solo puede demorar mucho el primer receive

- Simetrica (todos procesos se conocen con todos)
Mas corta y sencilla pero mayor numero de mensajes si no hay broadcast (acota el speedup)

- Tipo anillo (un proceso conoce a dos procesos, uno en el que manda otro en que recibe)
Nro lineal de mensajes, el ultimo tiene que esperar a que uno por uno computen, recorre 2 veces el anillo, bastante lento (casi secuencial)

---

# PMS
Canales tipo link
bloqueantes
unidireccional

no hay colas fifo

ojo con tema de la demora innecesaria -> es necesario un buffer

## CSP
Communicating Sequential Processes

comunicacion guardada (con booleans)

entrada -> query ?
salida -> bang !

puerto para identificar diferentes mensajes
```haskell
Proc[*]? -- permite recibir de cualquiera (NO TIENE ORDEN)
-- no se puede hacer con envio
```

### Comunicacion guardada
B;C->S;
- B de booleano, puede omitirse (si se omite es true)
- B y C forman la guarda
- La guarda tiene exito si B es true y ejecutar C no causa demora
- La guarda falla si B es false
- La guarda se bloquea si B es true y ejecutar C causa demora

**Evaluacion**
Si todas fallan el if/do termina sin efecto
Si una guarda es exitosa se elige de forma no deterministica
Si alguna se bloquea se espera hasta que alguna (cualquiera) tenga exito
**Ejecucion**
Si es exitosa ejecutar sentencia de comunicacion y luego las sentencias S

---

# Paradigmas de interaccion

## 1. Master/worker
clientes y servidor pero en MD
### Bag of tasks
- workers toman la tarea, la resuelven (posiblemente hacen nuevas tareas)
- master tiene la bag of tasks a la cual los workers le piden, tambien detecta fin de tareas

escalable y facil de equilibrar la carga de trabajo
## 2. Heartbeat
derivado de pares que interactuan
procesos periodicamente con los vecinos mas directos intercambiando informacion con mensajes send/receive
util para soluciones iterativas paralelizables
usa esquema divide and conquer distribuyendo la carga

envia a los vecinos directos la info local
recibe de los vecinos directos su info y va actualizando sus valores locales

comunicacion asincronica necesaria por temas de eficencia y evitar deadlock
## 3. Pipeline
derivado de filtros o productor y consumidor

canal de entrada -> procesa -> salida
workers operando en paralelo

lazo abierto w1 -> ... -> wN

circular w1 -> ... -> wN -> w1

cerrado (usando un coordinador)
 ## 4. Probes y echoes
interaccion entre procesos para recorrer grafos o arboles (tipo dfs) diseminado y juntando informacion

procesadores -> nodos
canales -> aristas

implementacion concurrente de dfs

manda mensaje (probe) en paralelo a los nodos sucesores, esperando una respuesta (echo)
en base a la respuesta va unificando la solucion
## 5. Broadcast
alcanzar informacion global en una arquitectura distribuida, sirve para toma de decisiones descentralizadas (no es tan facil de implementar como parece)

usando broadcast de red lan

problema es que el broadcast no es atomico y pueden ser recibidos en distinto orden
ordenacion a traves de relojes logicos
## 6. Token passing
arquitectura distribuida que recibe informacion global a traves de tokens o datos, permite la toma de decisiones distribuidas, uso de recursos etc

mensaje tipo token que otorga permiso para realizar una accion (exclusion mutua distribuida)
o
mensaje tipo token para recopilar informacion

## 7. Servidores replicados
servidores manejan mediante multiples instancias recursos compartidos

simular el uso de un unico recurso compartido que en realidad son varios por detras

- modelo centralizado: workers con un coordinador (decide acceso o no)
- modelo distribuido:  workers se comunican con 2 coordinadores (los 2 coord no se comunican entre ellos)
- modelo descentralizado: worker con un coordinador (se comunican entre ellos)

--- 

# RPC y Rendezvous

comunicacion bidireccional, sincronico, link
ideales para resolver aplicaciones cliente servidor

## RPC
modulos con procedures calleables para cada posible operacion y hay procesos background que son los que estan trabajando todo el tiempo; estos procesos se manejan con memoria compartida.
para la comunicacion al hacer un llamado a un procedure se crea un proceso que luego de ejecutarse se descarta.
```text
~
~
 \
  ~  -- luego muere
 /
~
~
```

RPC es solo un mecanismo de comunicacion, requiere una tecnica de sincronizacion:
- exclusion mutua (uno por vez a lo monitores, reduce demasiado concurrencia)
- concurrentemente (a lo semaforos)

RMI java

## Rendezvous 
procesos continuamente trabajando que pueden aceptar pedidos, resolverlos y devolver los resultados

Rendezvous combina comunicacion y sincronizacion

un cliente invoca una operacion por medio de un call pero es manejada por un proceso existente en vez de uno nuevo
```text
C  S
~  ~
~  ~
 \ .
   ~ 
 / ˙
~  ~
~  ~
```
