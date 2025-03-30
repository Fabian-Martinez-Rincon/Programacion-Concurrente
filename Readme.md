<div align="center"> <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&duration=1200&pause=1000&color=F78E23&center=true&width=435&lines=Programación Concurrente"/>

---

<a title="" href="https://youtu.be/WIjWz_u9zw8?si=RiKMh8NQzen1jrcD"><img src="/Documentos/image.png" width="550px"  /></a>

</div>




---

- [Explicaciones Teoricas](https://youtube.com/playlist?list=PLH8A0IjFldaGLATsgRdmPBtiNcp5KmAHo)
- [✅ Practica 1 Variables Compartidas](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica1.html)
- [✅ Practica 2 Semáforos](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica2.html)
- [✅ Practica 3 Monitores](https://fabian-martinez-rincon.github.io/Programacion-Concurrente/Documentos/Practica3.html)
- [Con esto aprobe el segundo parcial que contiene la practica 4 y 5](/Documentos/practica4-5.md)
- [Resumen para el primer Parcial](/Documentos/primer_parcial.md)

---

> El ultimo final para recibirme de Analista programador matar o morir


**📌 Preguntas Practicas FIJAS**

- [1) Calculos con Matrices](#1-calculos-con-matrices)
- [2) Cuales Cumplen con ASV](#2-cuales-cumplen-con-asv)
- [3) Cuales Cumplen con ASV 2](#3-cuales-cumplen-con-asv-2)
- [4) Numero de Mensajes y Granularidad](#4-numero-de-mensajes-y-granularidad)
- [5) Numero de Mensajes y Granularidad 2](#5-numero-de-mensajes-y-granularidad-2)
- [6) Indicar para cada item si son equivalentes](#6-indicar-para-cada-item-si-son-equivalentes)
- [7) ¿Que valores quedan?](#7-que-valores-quedan)
- [8) ¿Que valores quedan? 2](#8-que-valores-quedan-2)
- [9) La Solución a un problema es paralelizada](#9-la-solución-a-un-problema-es-paralelizada)
- [10) La Solución a un problema es paralelizada 2](#10-la-solución-a-un-problema-es-paralelizada-2)
- [11) La Solución a un problema es paralelizada 3](#11-la-solución-a-un-problema-es-paralelizada-3)
- [12) La Solución a un problema es paralelizada 4](#12-la-solución-a-un-problema-es-paralelizada-4)
- [13) Suponga que el tiempo de ejecución de un algoritmo Secuencial](#13-suponga-que-el-tiempo-de-ejecución-de-un-algoritmo-secuencial)
- [14) Suponga que el tiempo de ejecución de un algoritmo Secuencial 2](#14-suponga-que-el-tiempo-de-ejecución-de-un-algoritmo-secuencial-2)
- [15) Suponga que el tiempo de ejecución de un algoritmo Secuencial 3](#15-suponga-que-el-tiempo-de-ejecución-de-un-algoritmo-secuencial-3)
- [16) Calcular la suma de todos los valores](#16-calcular-la-suma-de-todos-los-valores)
- [17) Token passing con mensajes asincrónicos](#17-token-passing-con-mensajes-asincrónicos)

**📢 Miralas de Reojo**
- [1) Propuesta al problema de alocación SJN](#1-propuesta-al-problema-de-alocación-sjn)
- [2) “passing the condition” En Semaforos](#2-passing-the-condition-en-semaforos)
- [3) Problema de Concurrencia](#3-problema-de-concurrencia)
- [4) Problema de Concurrencia 2](#4-problema-de-concurrencia-2)
- [5) Indique los posibles valores finales de x](#5-indique-los-posibles-valores-finales-de-x)
- [6) Cuales valores de k son posibles](#6-cuales-valores-de-k-son-posibles)

**🚨 Rezar para que no Tomen**
- [1) Resuelva con monitores](#1-resuelva-con-monitores)
- [2) Protocolos de Acceso a la SC](#2-protocolos-de-acceso-a-la-sc)
- [3) Solución a la Criba](#3-solución-a-la-criba)
- [4) Transformar Solucion usando mensajes asincronicos](#4-transformar-solucion-usando-mensajes-asincronicos)
- [5) Problema de ordenar de menor a mayor un arreglo](#5-problema-de-ordenar-de-menor-a-mayor-un-arreglo)
- [6) Problema de ordenar de menor a mayor 2](#6-problema-de-ordenar-de-menor-a-mayor-2)
- [7) Suponga que un proceso productor y `n` procesos consumidores](#7-suponga-que-un-proceso-productor-y-n-procesos-consumidores)
- [8) Implemente una butterfly barrier para 8 procesos](#8-implemente-una-butterfly-barrier-para-8-procesos)
- [9) Suponga n^2 procesos organizados en forma de grilla cuadrada](#9-suponga-n2-procesos-organizados-en-forma-de-grilla-cuadrada)
- [10) Una imagen se encuentra representada por una matriz](#10-una-imagen-se-encuentra-representada-por-una-matriz)

---

# 📌 Preguntas Practicas FIJAS

<div align="center">
<img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjZ6M3Jubm13YjRyeHpxdmN5enp5cXhmdTZiMGhhaHRwbTAwMHo3NCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/yYT7ytuZpJjG0/giphy.gif" width="500px">
</div>

---

## 1) Calculos con Matrices

**Sea la siguiente solución al problema del producto de matrices de nxn con P procesos trabajando en paralelo.**

```cpp
process worker[w = 1 to P] {        // strips en paralelo (P strips de n/P filas)
    int first = (w - 1) * n / P;    // Primera fila del strip
    int last  = first + n / P - 1;  // Última fila del strip

    for (i = first to last) {
        for (j = 0 to n - 1) {
            c[i,j] = 0.0;
            for (k = 0 to n - 1)
                c[i,j] = c[i,j] + a[i,k] * b[k,j];
        }
    }
}
```

**a) Suponga que n = 128 y cada procesador es capaz de ejecutar un proceso. ¿Cuántas asignaciones, sumas y productos se hacen secuencialmente (caso en que P = 1)?**

<details><summary>👀 Respuesta</summary>

Si el algoritmo se ejecuta secuencialmente se tienen:

**Asignaciones**

- 128^3 + 128^2
- 2097152 + 16384
- 2113536

¿Por qué 128^3 y 128^2?

![image](https://github.com/user-attachments/assets/01115fc1-ec0a-4724-9c8c-e2d4f131e889)

**Sumas**

- 128^3
- 2097152

![image](https://github.com/user-attachments/assets/ae892334-82aa-4884-94d3-e8c1141fe745)


**Productos**
- 128^3
- 2097152

![image](https://github.com/user-attachments/assets/f81d5dd9-7a52-4786-88bd-0723be012499)


</details>

****b)** ¿Cuántas se realizan en cada procesador en la solución paralela con **P = 8**?**

<details><summary>👀 Respuesta</summary>

Si tenemos 8 procesos cada uno con un strip de 16 (128/8) los cálculos de tiempo quedarían para cada proceso como:

- La matriz de `C` es de tamaño `128x128`
- La estrategia paralela divide las **filas** de `C` entre **8 procesos**
- Y como hay `128` filas y `P=8`, cada proceso trabaja sobre `128/8` = `16 filas`

**Asignaciones con 8 procesos**

Anteriormente calculabamos las asignaciones de esta forma `128^3 + 128^2`, ahora vamos a hacer exactamente los mismo pero lo dividimos por la cantidad de procesos que tenemos

- Con `P=1` -> `128^3` + `128^2`
- Con `P=8` -> `(128^3)/8` + `(128^2)/8`

`(128^3)/8` + `(128^2)/8` <=> `128^2 * 16` + `128 * 16`

Podes usar la cuenta que quieras, son equivalentes, el resultado final te tendria que dar lo siguiente

- 262144 + 2048
- 264192

**Sumas**

- `(128^3)/8` <=> `128^2 * 16`
- 262144

**Productos**

- `(128^3)/8` <=> `128^2 * 16`
- 262144

</details>


**c)** Si los procesadores P1 a P7 son iguales, y sus tiempos de asignación son 1, de suma 2 y de producto 3, y si P8 es 4 veces más lento,  
- ¿Cuánto tarda el proceso total concurrente?  
- ¿Cuál es el valor del *speedup* (Tiempo secuencial / Tiempo paralelo)?  

Modifique el código para lograr un mejor *speedup*.

<details><summary>👀 Respuesta</summary>

**Problema Inicial: Distribución equitativa pero ineficiente**

Inicialmente, cada procesador **P1** a **P8** procesa la misma cantidad de filas de la matriz. Dado que la matriz es de tamaño **128×128**, se divide en **8 partes iguales**, lo que significa que cada procesador maneja **16 filas**.

> P1 a P8 tienen igual número de operaciones.
> Es como tener 8 autos y a uno le faltan dos ruedas

- **Asignaciones** -> `264192`
- **Sumas** -> `262144`
- **Producto** -> `262144`

Los tiempos de ejecución para **P1** a **P7** son:

- T(P1-P7)
- (`264192` x 1) + (`262144` x 2) + (`262144` x 3)
- `264192` + `524288` + `786432` = 1574912

Sin embargo, P8 es 4 veces más lento, por lo que su tiempo total de ejecución es

- T(P8)
- 1574912 x 4
- `6299648`

Como el tiempo de ejecución total en paralelo está determinado por el procesador más lento, el tiempo total de ejecución es:

Cálculo del speedup inicial:

T(Secuencial) = 1574912 * 8  -> 12.599.296

- Speedup
- T(secuencial)/ T(paralelo)
- (1574912 * 8) / (1574912 x 4)
- 2

> 🔴 Problema:
> Aunque tenemos 8 procesadores, el speedup es solo 2, lo cual es muy bajo. Esto ocurre porque P8, al ser más lento, arruina la eficiencia del paralelismo.

**Objetivo del Balance de Carga**

La solución al problema es redistribuir la carga de trabajo para que `P8` tenga menos filas, y así termine aproximadamente en el mismo tiempo que `P1-P7`.

Queremos encontrar cuántas filas `𝑓` debe procesar `P8` para que su tiempo total sea igual al tiempo de ejecución de `P1-P7`.

Sabemos que el tiempo de ejecución de un procesador depende del número de filas que procesa.

Como `P8` es `4` veces más lento, su tiempo de ejecución será:

> Formula original n=128/8  -> 16 Filas

![image](https://github.com/user-attachments/assets/2f0c423e-94bc-41df-82d1-8f086635ed76)

- Calculamos f
- f/16 x 4 = 1
- f x 4 = 16
- f = 16/4
- f = 4

> Por lo tanto, P8 debe procesar solo 4 filas.

**Redistribución de Filas en P1-P7**

Ahora que sabemos que P8 debe procesar 4 filas, debemos redistribuir las filas restantes entre los otros procesadores.

- Total de filas en la matriz: 128
- Filas asignadas a P8: 4
- Filas restantes para los demás procesadores:

128 − 4 = 124

Distribuimos estas filas entre los 7 procesadores restantes (P1-P7):

- `124/7` = 17.71 ≈ 18

Creeeeo que esta bien, aca esta otra respuesta

![image](https://github.com/user-attachments/assets/5efe7df8-630b-4df3-81f1-96fb8f792f80)

</details>

---

## 2) Cuales Cumplen con ASV

Dado el siguiente programa concurrente con memoria compartida:  
`x := 4; y := 2; z := 3;`

```cpp
co
   x := x - z;
   z := z * 2;
   y := z + 4
oc
```

**a) ¿Cuáles de las asignaciones dentro de la sentencia `co` cumplen la propiedad de ASV? Justifique claramente.**

<details><summary>👀 Respuesta</summary>

```cpp
Co
    X := X - Z
    Z := Z * 2
    Y := Z + 4
Oc
```

**📌 Recordatorio: ¿Qué es ASV?**

Una asignación `x := e` **cumple la propiedad de ASV** si:

- ✅ (1) `e` contiene **a lo sumo una referencia crítica**, **y** la variable `x` (la que se asigna) **no es usada en otros procesos**,  
**o**
- ✅ (2) `e` **no contiene ninguna referencia crítica**.


**🧠 ¿Qué es una *referencia crítica*?**

Es cualquier acceso (lectura o escritura) a una variable **compartida entre procesos concurrentes**.  
Si una variable aparece en más de una instrucción dentro del bloque `Co ... Oc`, entonces es **crítica**.


**`1)`** `X := X - Z`

```
Co
    X := X - Z
    Z := Z * 2
    Y := Z + 4
Oc
```

- `Variables involucradas:`
    - Lee `X` y `Z`
    - Asigna a `X`
- **`¿Referencias críticas?`**
    - `Z` también aparece en otras asignaciones (`Z := Z * 2`, `Y := Z + 4`) → **Sí**, es crítica  
    - `X` **no aparece en ninguna otra instrucción** → **No es crítica**
- **`Evaluación ASV`**:
    - Tiene **una sola referencia crítica** (`Z`)
    - La variable asignada (`X`) **no se usa en otro proceso**

✅ **Cumple ASV**


**`2)`** `Z := Z * 2`

```
Co
    X := X - Z
    Z := Z * 2
    Y := Z + 4
Oc
```

- **`Variables involucradas:`**
    - Lee y escribe `Z`
- **`¿Referencias críticas?`**
    - `Z` aparece también en:
      - `X := X - Z`
      - `Y := Z + 4`
    - **Z es usada en múltiples procesos** → **es crítica**
    - Además, se está modificando en esta instrucción → escritura
- **`Evaluación ASV`**
    - Tiene **una referencia crítica** (`Z`)
    - La variable asignada (`Z`) **sí se usa en otros procesos**

❌ **No cumple ASV**

**`3)`** `Y := Z + 4`

 Variables involucradas:
- Lee `Z`
- Asigna a `Y`

 ¿Referencias críticas?
- `Z` es crítica (como ya dijimos)
- `Y` **no aparece en ningún otro proceso**

 Evaluación ASV:
- Tiene **una sola referencia crítica** (`Z`)
- La variable asignada (`Y`) **no se usa en otros procesos**

✅ **Cumple ASV**

| Instrucción      | ¿Cumple ASV? | Justificación                                                                 |
|------------------|--------------|--------------------------------------------------------------------------------|
| `X := X - Z`     | ✅ Sí         | Tiene una única referencia crítica (`Z`), y `X` no es usada en otros procesos |
| `Z := Z * 2`     | ❌ No         | Tiene referencia crítica (`Z`), y `Z` es usada en otros procesos              |
| `Y := Z + 4`     | ✅ Sí         | Tiene una única referencia crítica (`Z`), y `Y` no es usada en otros procesos |

> A chequear

</details>

****b)** Indique los resultados posibles de la ejecución. Justifique.**

<details><summary>👀 Respuesta</summary>

```
x = 3; y = 2; z = 5;
Co
    X := X - Z
    Z := Z * 2
    Y := Z + 4
Oc
```

| Orden de ejecución | Operaciones realizadas (con valores) | Resultado final `(X, Z, Y)` |
|--------------------|---------------------------------------|------------------------------|
| **T1 → T2 → T3**   | `X = 4 - 3 = 1`<br>`Z = 3 * 2 = 6`<br>`Y = 6 + 4 = 10` | **(1, 6, 10)** |
| **T1 → T3 → T2**   | `X = 4 - 3 = 1`<br>`Y = 3 + 4 = 7`<br>`Z = 3 * 2 = 6` | **(1, 6, 7)** |
| **T2 → T1 → T3**   | `Z = 3 * 2 = 6`<br>`X = 4 - 6 = -2`<br>`Y = 6 + 4 = 10` | **(-2, 6, 10)** |
| **T2 → T3 → T1**   | `Z = 3 * 2 = 6`<br>`Y = 6 + 4 = 10`<br>`X = 4 - 6 = -2` | **(-2, 6, 10)** |
| **T3 → T1 → T2**   | `Y = 3 + 4 = 7`<br>`X = 4 - 3 = 1`<br>`Z = 3 * 2 = 6` | **(1, 6, 7)** |
| **T3 → T2 → T1**   | `Y = 3 + 4 = 7`<br>`Z = 3 * 2 = 6`<br>`X = 4 - 6 = -2` | **(-2, 6, 7)** |



- `X := 4 - Z` → depende del valor de `Z` al momento de ejecutar T1
- `Y := Z + 4` → depende del valor de `Z` al momento de ejecutar T3
- `Z := Z * 2` → siempre lleva `Z` de 3 a 6

El valor de Z es siempre el mismo ya que no posee ninguna referencia crítica. Los valores de X e Y se ven afectados por la ejecución de T2 ya que sus resultados dependen de la referencia que hacen a la variable Z que es modificada. Entonces, si T1 y T3 se ejecutan antes que T2 ambas usarán el valor inicial de Z que es 3 obteniendo los resultados X=1 e Y=7; ahora si T2 se ejecuta antes que las demás los resultados serán X=-2 e Y=10 y por último, tenemos los casos en que T2 se ejecuta en medio con T1 antes y T3 después o con T3 antes y T1 después.

- Nota 1: las instrucciones NO SON atómicas.
- Nota 2: no es necesario que liste TODOS los resultados.

> Se podria consultar esto

</details>

---

## 3) Cuales Cumplen con ASV 2

Dado el siguiente programa concurrente con memoria compartida:  

`x = 3; y = 2; z = 5;`

```cpp
co
    x = y * z
    z = z * 2
    y = y + 2x
oc
```

**a) ¿Cuáles de las asignaciones dentro de la sentencia `co` cumplen la propiedad de “A lo sumo una vez”? Justifique claramente.**

<details><summary>👀 Respuesta</summary>

Siendo:
```
A: x = y * z  Tiene 2 referencias críticas (a y, a z), por lo tanto no cumple ASV. (además x es leída en en C.)
B: z = z * 2 No tiene referencia crítica y es leída por otro (en A se lee z), por lo tanto cumple ASV.
C: y = y + 2x Tiene 1 referencia crítica (a x) y además es leída por otro proceso (en A se lee y), por lo tanto no cumple ASV.
```

> A chequear
</details>


****b)** Indique los resultados posibles de la ejecución. Justifique.**

<details><summary>👀 Respuesta</summary>

| **#** | **Orden de ejecución**             | **Operaciones realizadas**                                                                                                                                         | **Resultado final**            |
|------:|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|
| 1     | A → B → C                          | `x = 2*5 = 10`<br>`z = 5*2 = 10`<br>`y = 2 + 2*10 = 22`                                                                                                             | `x = 10`, `z = 10`, `y = 22`  |
| 2     | A → C → B                          | `x = 2*5 = 10`<br>`y = 2 + 2*10 = 22`<br>`z = 5*2 = 10`                                                                                                             | `x = 10`, `z = 10`, `y = 22`  |
| 3     | C → B → A                          | `y = 2 + 2*3 = 8`<br>`z = 5*2 = 10`<br>`x = 2*10 = 20`                                                                                                              | `x = 20`, `z = 10`, `y = 8`   |
| 4     | B → C → A                          | `z = 5*2 = 10`<br>`y = 2 + 2*3 = 8`<br>`x = 2*10 = 20`                                                                                                              | `x = 20`, `z = 10`, `y = 8`   |
| 5     | C → A → B                          | `y = 2 + 2*3 = 8`<br>`x = 2*5 = 10`<br>`z = 5*2 = 10`                                                                                                               | `x = 10`, `z = 10`, `y = 8`   |
| 6     | B → A → C                          | `z = 5*2 = 10`<br>`x = 2*10 = 20`<br>`y = 2 + 2*20 = 42`                                                                                                            | `x = 20`, `z = 10`, `y = 42`  |
| 7     | A lee `y=2`, C lee `x=3`, luego A termina, luego B | `A empieza: y=2`<br>`C: y = 2 + 2*3 = 8`<br>`A termina: x = 2*5 = 10`<br>`B: z = 5*2 = 10`                                 | `x = 10`, `z = 10`, `y = 8`   |
| 8     | A lee `y=2`, C lee `x=3`, luego B, luego A termina | `A empieza: y=2`<br>`C: y = 2 + 2*3 = 8`<br>`B: z = 5*2 = 10`<br>`A termina: x = 2*10 = 20`                                 | `x = 20`, `z = 10`, `y = 8`   |

</details>

---

## 4) Numero de Mensajes y Granularidad

**Suponga los siguientes programas concurrentes. Asuma que “función” existe, y que los procesos son iniciados desde el programa principal.**

<table>
<tr><td>P1</td><td>P2</td></tr>
<tr><td>

```cpp
chan canal (double);

process grano1 {
    int veces, i;
    double sum;

    for (veces = 1 to 10) {
        for (i = 1 to 10000)
            sum = sum + funcion(i);
        send canal(sum);
    }
}

process grano2 {
    int veces;
    double sum;

    for (veces = 1 to 10) {
        receive canal(sum);
        printf(sum);
    }
}
```
</td><td>

```cpp
chan canal (double);

process grano1 {
    int veces, i;
    double sum;

    for (veces = 1 to 10000) {
        for (i = 1 to 10)
            sum = sum + i;
        send canal(sum);
    }
}

process grano2 {
    int veces;
    double sum;

    for (veces = 1 to 10000) {
        receive canal(sum);
        printf(sum);
    }
}
```
</td></tr>
</table>

**a) Analice desde el punto de vista del número de mensajes.**

<details><summary>Respuesta</summary>

En ambos programas, el canal `canal` se utiliza para **comunicar el resultado parcial `sum`** desde `grano1` hacia `grano2`, mediante un mensaje por cada iteración externa del bucle principal en `grano1`.

- **En P1**, el proceso `grano1` ejecuta un bucle externo de **10 iteraciones**, y en cada una de ellas calcula la suma de `funcion(i)` para `i = 1 a 10000`, y luego envía un solo mensaje con ese resultado a `grano2`.  
  🔸 Por lo tanto, **se envían 10 mensajes** en total.

- **En P2**, el proceso `grano1` ejecuta un bucle externo de **10000 iteraciones**, y en cada una de ellas suma los números del 1 al 10 y luego **envía un mensaje por iteración** a `grano2`.  
  🔸 En este caso, **se envían 10000 mensajes** en total.

🔍 **Conclusión:**  
Desde el punto de vista de la cantidad de mensajes transmitidos:
- **P1 es más eficiente**, ya que comunica sólo 10 veces.
- **P2 genera una sobrecarga mucho mayor**, con 10000 envíos de mensajes.


</details>

**b) Analice desde el punto de vista de la granularidad de los procesos.**

<details><summary>Respuesta</summary>

En **P1**, el envío de los mensajes se realiza después de largos períodos de ejecución ya que entre cada **send** se ejecuta una iteración de **10000** unidades de tiempo, esto nos asegura que la comunicación entre los dos procesos es poco frecuente.

Dadas dichas características podemos decir, que desde el punto de vista de la **granularidad**, **P1** es de **granularidad gruesa** ya que la comunicación ente los procesos **no es de manera reiterada**.

Al tener mayor granularidad disminuye la concurrencia y la sobrecarga de bloqueos.

En **P2**, el envío de mensajes se realiza en intervalos cortos de tiempo (entre la ejecución de cada send sólo se ejecuta un **for de 1 a 10**), aumentando considerablemente la comunicación respecto de **P1**.

Por lo tanto, podemos decir que **P2** es de **granularidad fina**, ya que en cada iteración el volumen de comunicación aumenta, por lo tanto la relación cómputo / comunicación disminuye. Al disminuir la **granularidad** aumenta la **concurrencia** pero también aumenta la **sobrecarga de bloqueos**.
</details>

<details><summary>Prioridad y Granularidad</summary>

![alt text](/images/image-7.png)
</details>

> Tengo la duda de cual es la diferencia entre el **grano fino** y el **grano grueso**

**c) Cuál de los programas le parece más adecuado para ejecutar sobre una arquitectura de tipo cluster de PCs? Justifique.**

<details><summary>Respuesta</summary>

La implementación más adecuada para este tipo de arquitecturas es **P1**, por ser de **granularidad gruesa**. Al tratarse de una arquitectura con memoria distribuida la comunicación entre los procesos es más costosa ya que cada proceso puede ejecutarse
en computadores diferentes, por lo tanto sería más eficiente que la sobrecarga de
comunicación sea lo más baja posible, y dicha característica la brinda la **granularidad gruesa**.

</details>

---

## 5) Numero de Mensajes y Granularidad 2

Suponga los siguientes programas concurrentes. Asuma que **EOS** es un valor especial que indica el **fin de la secuencia de mensajes**, y que los procesos son iniciados desde el programa principal.

<table>
<tr><td>P1</td><td>P2</td></tr>
<tr><td>

```cpp
chan canal (double);

process Genera {
    int fila, col;
    double sum;

    for (fila = 1 to 10000) {
        for (col = 1 to 10000)
            send canal(a(fila, col));
    }

    send canal(EOS);  // End of Stream
}

process Acumula {
    double valor, sumT;
    sumT = 0;

    receive canal(valor);
    while (valor <> EOS) {
        sumT = sumT + valor;
        receive canal(valor);
    }

    printf(sumT);
}
```
</td><td>

```cpp
chan canal (double);

process Genera {
    int fila, col;
    double sum;

    for (fila = 1 to 10000) {
        sum = 0;
        for (col = 1 to 10000)
            sum = sum + a(fila, col);
        send canal(sum);
    }
    send canal(EOS);  // End of Stream
}

process Acumula {
    double valor, sumT;
    sumT = 0;
    receive canal(valor);
    while (valor <> EOS) {
        sumT = sumT + valor;
        receive canal(valor);
    }

    printf(sumT);
}

```
</td></tr>
</table>

**a) ¿Qué hacen los programas?**

<details><summary>Respuesta</summary>

Ambos programas tienen como objetivo calcular la **suma total de todos los elementos de una matriz** de tamaño 10000×10000. La diferencia principal radica en **dónde se realiza la mayor parte del trabajo de acumulación**.

- En **P1**, el proceso `Genera` envía **cada elemento individual** de la matriz (es decir, 10000 × 10000 = 100 millones de mensajes) al proceso `Acumula`, el cual es el encargado de realizar la suma total.  
  👉 En este caso, la carga de cómputo recae completamente en `Acumula`.

- En **P2**, el proceso `Genera` **suma localmente cada fila** de la matriz y luego envía **solo un valor por fila** (la suma de esa fila) al proceso `Acumula`. Como hay 10000 filas, `Genera` envía **solo 10000 mensajes**.  
  👉 Aquí, `Genera` hace parte del trabajo de acumulación, y `Acumula` solo se encarga de sumar 10000 valores (uno por fila).

🔍 **Conclusión**: Ambos programas calculan la suma total de la matriz, pero **P2 es más eficiente** en cuanto a **comunicación y carga de trabajo**, ya que reduce drásticamente el número de mensajes enviados por el canal.

</details>

**b) Analice desde el punto de vista del número de mensajes.**

<details><summary>Respuesta</summary>

Desde el punto de vista del número de mensajes enviados por el proceso `Genera` al proceso `Acumula`:

- En **P1**, se envía **un mensaje por cada elemento** de la matriz de 10000 × 10000, lo que da un total de **100 millones de mensajes**.  
  👉 Esto representa una alta carga de comunicación.

- En **P2**, se realiza **un solo mensaje por fila**, ya que `Genera` acumula localmente la suma de cada fila y luego envía ese resultado. Por lo tanto, se envían únicamente **10000 mensajes**.  
  👉 Esto reduce considerablemente la cantidad de mensajes en comparación con P1.

🔍 **Conclusión**: **P2 es mucho más eficiente en términos de comunicación**, ya que reduce el número de mensajes de 100 millones a solo 10000.

</details>

**c) Analice desde el punto de vista de la granularidad de los procesos.**

<details><summary>Respuesta</summary>

Desde el punto de vista de la granularidad, el programa **P2** presenta una **granularidad más gruesa** que **P1**. Esto se debe a que en P2 el proceso `Genera` realiza una mayor cantidad de cómputo local (acumula la suma de cada fila) antes de comunicarse con el proceso `Acumula`.

En cambio, en **P1**, `Genera` realiza un procesamiento mínimo y se limita a enviar cada valor individual al acumulador, generando así una gran cantidad de comunicaciones.

🔍 **Conclusión**:  
Al realizar más procesamiento local y reducir la frecuencia de comunicación, **P2 tiene un grano más grueso**, lo cual generalmente implica **mejor eficiencia y menor sobrecarga de comunicación** en sistemas concurrentes.

</details>

<details><summary>🧩 ¿Qué es la granularidad?</summary>

La **granularidad** de una aplicación concurrente o paralela se refiere a la **relación entre el tiempo dedicado al cómputo y el tiempo dedicado a la comunicación** entre procesos o hilos.

- Si una aplicación realiza **mucho cómputo local** antes de necesitar comunicarse, se dice que tiene **grano grueso**.
- Si, por el contrario, realiza **frecuentes comunicaciones** con poco cómputo entre medio, se dice que tiene **grano fino**.

Esta característica es clave para el **diseño y rendimiento** de programas paralelos, ya que:
- **Grano grueso** suele ser más eficiente en arquitecturas donde la comunicación es costosa.
- **Grano fino** puede aprovechar mejor arquitecturas con alta velocidad de comunicación o memoria compartida eficiente.

🔧 **Resumen**:  
> La granularidad es la proporción entre el cómputo y la comunicación en una aplicación. Afecta cómo se adapta el programa a una arquitectura paralela, diferenciándose entre **grano fino** (más comunicación) y **grano grueso** (más procesamiento local).

</details>

**d) ¿Cuál de los programas le parece más adecuado para ejecutar sobre una arquitectura de tipo cluster de PCs? Justifique.**

<details><summary>Respuesta</summary>

Las arquitecturas tipo **cluster de PCs** se caracterizan por estar compuestas por múltiples nodos con alta capacidad de cómputo, pero con **canales de comunicación relativamente lentos** y costosos en comparación con arquitecturas compartidas.

Por esta razón, se consideran arquitecturas de **grano grueso**, ya que se adaptan mejor a programas que realizan **mucho procesamiento local** y **reducen al mínimo la comunicación entre procesos**.

En este contexto, el programa **P2** resulta más adecuado para ejecutarse en un cluster, ya que `Genera` acumula localmente la suma de cada fila y envía solo **un valor por fila**, reduciendo significativamente la cantidad de mensajes enviados (de 100 millones a 10.000).

🔍 **Conclusión**:  
> **P2 es más apropiado para ejecutarse sobre arquitecturas tipo cluster**, ya que aprovecha mejor el cómputo local y minimiza la necesidad de comunicación, alineándose con las características de este tipo de sistema.

</details>

---

## 6) Indicar para cada Item si son Equivalentes

Dados los siguientes dos segmentos de codigo, indicar para cada uno de los ítems si son equivalentes o no. Justificar cada caso (de ser necesario dar ejemplos).

<table><td>

```cpp
...
int cant = 1000;

DO 
  (cant < -10); datos?(cant) → Sentencias1
▭ (cant > 10);  datos?(cant) → Sentencias2
▭ (INCOGNITA);  datos?(cant) → Sentencias3
END DO
...
```
</td><td>

```cpp
...
int cant = 1000;

While (true) {
  IF (cant < -10); datos?(cant) → Sentencias1
  ▭  (cant > 10);  datos?(cant) → Sentencias2
  ▭  (INCOGNITA); datos?(cant) → Sentencias3
END IF}
...
```
</td></table>

<details><summary>Respuesta</summary>

En ambos segmentos, inicialmente la variable `cant` tiene el valor 1000. Por lo tanto, la ejecución comienza evaluando la guarda `(cant > 10)`, que es verdadera, y se ejecutan las acciones asociadas a esa rama (por ejemplo, `Sentencias2`).

Sin embargo, si durante la ejecución de esa rama el valor de `cant` cambia (ya sea por una asignación directa o por un valor recibido por el canal), entonces **las guardas deben estar definidas de manera que contemplen todos los posibles valores que `cant` pueda tomar**, para asegurar que el comportamiento de ambos segmentos sea equivalente.

De lo contrario, puede suceder que en **el Segmento 1** todas las guardas resulten falsas y, en ese caso, el `DO` se termina y la ejecución del programa continúa normalmente. En cambio, en **el Segmento 2**, como se trata de un bucle infinito (`while (true)`), si ninguna guarda es verdadera, el programa queda bloqueado esperando indefinidamente, a menos que `cant` sea modificada por otro proceso o evento externo.

🔍 **Conclusión**:  
Para que ambos segmentos sean equivalentes, es fundamental que las guardas consideren **todos los posibles valores** que puede tomar `cant`, incluyendo un caso **por defecto (catch-all)** como la **INCOGNITA**, que permita garantizar siempre una rama ejecutable.

</details>

**a) INCOGNITA equivale a: (cant = 0)**

<details><summary>Respuesta</summary>

Los segmentos **no son equivalentes**. En el **Segmento 1**, el uso de la estructura `DO` implica que si **ninguna de las guardas** se cumple (por ejemplo, si `cant` toma valores entre -10 y 10 excluyendo el 0), entonces el bloque termina y la ejecución del programa continúa.

En cambio, en el **Segmento 2**, el bucle es un `while (true)`, por lo que **aunque ninguna guarda sea verdadera**, el ciclo continuará intentando evaluarlas en cada iteración. Esto provoca una diferencia clave en el comportamiento:  
- El **Segmento 1** puede **finalizar naturalmente** si no hay guardas habilitadas.  
- El **Segmento 2** puede **quedar bloqueado indefinidamente**, esperando que alguna condición se cumpla, a menos que `cant` se modifique desde otro proceso.

🔍 **Conclusión:**  
Para que ambos segmentos sean equivalentes, es necesario que las guardas cubran **todos los posibles valores de `cant`**, y en ese sentido, usar `(cant = 0)` como **INCOGNITA** ayuda a completar el conjunto de condiciones evaluables.

</details>

<details><summary>🛡️ ¿Qué es una guarda?</summary>

Una **guarda** es una **condición lógica** que se asocia a una acción (como el envío o recepción de un mensaje, o la ejecución de una sentencia) y que **debe cumplirse para que esa acción se realice**.

En programación concurrente y modelos como **Comunicación por Paso de Mensajes (CSP), Guarded Commands (Dijkstra), ADA**, etc., las guardas permiten controlar **cuándo** se puede ejecutar una determinada rama del código.

🔍 **Ejemplo clásico:**

```cpp
DO
  (x > 0) → acción1;
▭ (y == 3) → acción2;
OD
```

En este caso:
- `(x > 0)` y `(y == 3)` son **guardas**.
- Solo se ejecutan las acciones **cuyas guardas sean verdaderas**.
- Si más de una guarda se cumple, el sistema puede elegir **nondeterminísticamente** cuál ejecutar.
- Si **ninguna guarda se cumple**, el proceso queda bloqueado o (dependiendo del lenguaje) termina.

✅ **En resumen:**

> Una **guarda** es una condición que **habilita o bloquea** la ejecución de una acción. Se utiliza para expresar **comportamientos condicionales** en sistemas concurrentes o reactivos, y es clave para controlar la sincronización y el flujo de ejecución.

</details>

**b) INCOGNITA equivale a: (cant > -100)**

<details><summary>Respuesta</summary>

Con esta condición, ambos segmentos se vuelven **equivalentes** en términos de comportamiento.

Esto se debe a que la guarda `(cant > -100)` **cubre todos los casos restantes** no contemplados por las otras guardas `(cant < -10)` y `(cant > 10)`. Por lo tanto, **siempre habrá al menos una guarda habilitada**, sin importar el valor de `cant`.

Como consecuencia:
- En el **Segmento 1**, el bucle `DO` **nunca finaliza**, ya que nunca se da una situación donde todas las guardas sean falsas.
- En el **Segmento 2**, el bucle `while (true)` tampoco se detiene, y siempre ejecutará una de las ramas del `IF`.

🔍 **Conclusión:**  
Ambos segmentos ejecutan indefinidamente y responden de forma equivalente a los distintos valores de `cant`, ya que las guardas **cubren todos los casos posibles**.

</details>

**c) INCOGNITA equivale a: ((cant > 0) or (cant < 0))**

<details><summary>Respuesta</summary>

Con esta condición, los segmentos **no son equivalentes**.

La razón es que cuando `cant = 0`, **ninguna de las tres guardas** se cumple:
- `(cant < -10)` → **falsa**
- `(cant > 10)` → **falsa**
- `((cant > 0) OR (cant < 0))` → **falsa**, ya que `cant = 0`

Entonces:
- En el **Segmento 1**, si todas las guardas son falsas (como ocurre con `cant = 0`), el bucle `DO` finaliza, y la ejecución continúa con el resto del programa.
- En el **Segmento 2**, el bucle `while (true)` permanece activo, pero al no cumplirse ninguna guarda, el programa queda bloqueado esperando que `cant` cambie, lo que puede requerir la intervención de otro proceso.

🔍 **Conclusión:**  
> Dado que el comportamiento ante `cant = 0` **no es el mismo en ambos segmentos**, se concluye que **no son equivalentes**.

</details>

**d) INCOGNITA equivale a: ((cant > -10) or (cant < 10))**

<details><summary>Respuesta</summary>

Con esta condición, los segmentos **no son equivalentes**.

Esto se debe a que, cuando `cant = 10` o `cant = -10`, **ninguna de las guardas se cumple**:

- `(cant < -10)` → **falsa**
- `(cant > 10)` → **falsa**
- `((cant > -10) OR (cant < 10))` → **falsa**  
  > Porque `cant = 10` y `cant = -10` no satisfacen **ni** `cant > -10` (en el caso de -10) **ni** `cant < 10` (en el caso de 10) al mismo tiempo, y la expresión en realidad se evalúa como ambigua o mal definida según cómo se interprete.  
  Aunque matemáticamente parece abarcar todo, **en este contexto**, deja afuera justo los valores límite.

Como consecuencia:
- En el **Segmento 1**, si ninguna guarda es verdadera (por ejemplo, para `cant = 10` o `cant = -10`), el bucle `DO` termina.
- En el **Segmento 2**, el bucle `while (true)` continúa ejecutándose, pero al no cumplirse ninguna condición, queda bloqueado hasta que `cant` cambie.

🔍 **Conclusión:**  
> Dado que para ciertos valores (`cant = 10` o `cant = -10`) el `DO` termina en el Segmento 1 pero el `while` no en el Segmento 2, los segmentos **no son equivalentes**.

</details>

**e) INCOGNITA equivale a: ((cant >= -10) or (cant <= 10))**

<details><summary>Respuesta</summary>

Con esta condición, los segmentos se vuelven **equivalentes**.

Esto se debe a que la nueva guarda cubre **todos los valores posibles de `cant`** que no están contemplados por las otras dos guardas:

- `(cant < -10)`
- `(cant > 10)`

Con `INCOGNITA = ((cant >= -10) OR (cant <= 10))`, se incluyen justamente los valores **`cant = -10` y `cant = 10`**, que en el caso anterior (ítem d) quedaban fuera, provocando que todas las guardas fueran falsas y el `DO` terminara.

Ahora, al asegurarse que **siempre al menos una guarda es verdadera**, el `DO` del **Segmento 1** nunca finaliza, lo que hace que el comportamiento sea **equivalente al `while(true)` del Segmento 2**, donde la ejecución es continua mientras alguna condición sea válida.

🔍 **Conclusión:**  
> Con esta guarda, los segmentos **son equivalentes**, ya que **se garantiza que siempre al menos una rama es ejecutable**, y por lo tanto, el ciclo no se interrumpe inesperadamente.

</details>

---

## 7) ¿Que valores quedan?


**4.** Dado el siguiente bloque de código, indique para cada inciso qué valor queda en `aux`, o si el código queda bloqueado. Justifique sus respuestas.

```pascal
aux := -1;
...
if (A == 0); P2?(aux) → aux = aux + 2;
▭ (A == 1); P3?(aux) → aux = aux + 5;
▭ (B == 0); P3?(aux) → aux = aux + 7;
end if;
```

<details><summary><strong>i. Si el valor de A = 1 y B = 2 antes del if, y solo P2 envia el valor 6.</strong></summary>

🔍 **Análisis:**

- Las guardas evaluadas son:
  - `(A == 0)` → **falsa**
  - `(A == 1)` → **verdadera**
  - `(B == 0)` → **falsa**

- Solo **una guarda es verdadera**: `(A == 1)`, que corresponde a la rama `P3?(aux) → aux = aux + 5`.

- Sin embargo, **P3 no ha enviado ningún valor**, por lo tanto, el proceso **queda bloqueado esperando** que `P3` envíe un valor.

✅ **Conclusión:**
> El código queda **bloqueado** en la única rama habilitada, porque **P3 no se ejecutó**.

</details>


<details><summary><strong>ii. Si el valor de A = 0 y B = 2 antes del if, y solo P2 envia el valor 8.</strong></summary>

🔍 **Análisis:**

- Guardas evaluadas:
  - `(A == 0)` → **verdadera**
  - `(A == 1)` → falsa
  - `(B == 0)` → falsa

- Solo la **primera guarda** es válida: `(A == 0); P2?(aux) → aux = aux + 2`.
- Como **P2 envía el valor 8**, el proceso puede recibirlo y ejecuta `aux = 8 + 2`.

✅ **Resultado:**
> El valor final de `aux` será **10**, y el código **no queda bloqueado**.

</details>

<details><summary><strong>iii. Si el valor de A = 2 y B = 0 antes del if, y solo P3 envia el valor 6.</strong></summary>

🔍 **Análisis:**

- Guardas evaluadas:
  - `(A == 0)` → falsa
  - `(A == 1)` → falsa
  - `(B == 0)` → **verdadera**

- Solo la **tercera guarda** es válida: `(B == 0); P3?(aux) → aux = aux + 7`.

- Como **P3 envía el valor 6**, el proceso lo recibe y ejecuta `aux = 6 + 7`.

✅ **Resultado:**
> El valor final de `aux` será **13**, y el código **no queda bloqueado**.

</details>

<details><summary><strong>iv. Si el valor de A = 2 y B = 1 antes del if, y solo P3 envia el valor 9.</strong></summary>

🔍 **Análisis:**

- Guardas evaluadas:
  - `(A == 0)` → falsa
  - `(A == 1)` → falsa
  - `(B == 0)` → falsa

- Ninguna de las guardas es verdadera, por lo tanto, **el bloque `if` no se ejecuta**.

✅ **Resultado:**
> El código **no se bloquea**, pero **no ejecuta ninguna acción**. El valor de `aux` **se mantiene en -1**.

</details>

<details><summary><strong>v. Si el valor de A = 1 y B = 0 antes del if, y solo P3 envia el valor 14.</strong></summary>

🔍 **Análisis:**

- Guardas evaluadas:
  - `(A == 0)` → falsa  
  - `(A == 1)` → **verdadera** → `P3?(aux) → aux = aux + 5`
  - `(B == 0)` → **verdadera** → `P3?(aux) → aux = aux + 7`

- Hay **dos guardas verdaderas**, y ambas comparten el **mismo canal `P3?(aux)`**, por lo tanto, se produce una **elección no determinista** entre ambas ramas.

- Como **P3 envía el valor 14**, cualquiera de las dos ramas puede ejecutarse:

  - Si se elige la rama `(A == 1)`, entonces `aux = 14 + 5 = 19`.
  - Si se elige la rama `(B == 0)`, entonces `aux = 14 + 7 = 21`.

✅ **Resultado:**
> El código **no se bloquea**, y el valor de `aux` puede ser **19 o 21**, dependiendo de **cuál rama se elija** de forma no determinista.

</details>


<details><summary><strong>vi. Si el valor de A = 0 y B = 0 antes del if, P3 envia el valor 9 y P2 el valor 5.</strong></summary>

🔍 **Análisis:**

- Guardas evaluadas:
  - `(A == 0)` → **verdadera** → `P2?(aux) → aux = aux + 2`
  - `(A == 1)` → falsa
  - `(B == 0)` → **verdadera** → `P3?(aux) → aux = aux + 7`

- Hay **dos guardas verdaderas**, cada una con un canal distinto (`P2` y `P3`), y **ambos procesos han enviado un valor**, por lo tanto **no hay bloqueo**.

- Como hay dos ramas habilitadas, se produce una **elección no determinista** entre:
  - Recibir `5` de **P2** y hacer `aux = 5 + 2 = 7`
  - Recibir `9` de **P3** y hacer `aux = 9 + 7 = 16`

✅ **Resultado:**
> El código **no queda bloqueado**, y el valor de `aux` puede ser **7 o 16**, dependiendo de cuál rama se elija de forma no determinista.

</details>

<details><summary><strong>Resumen de todo</strong></summary>

| Inciso | Valores Iniciales (`A`, `B`) | Canales Activos         | Guardas Verdaderas                 | ¿Bloqueo? | Valor final de `aux`      | Observación                                 |
|--------|-------------------------------|--------------------------|-------------------------------------|-----------|----------------------------|----------------------------------------------|
| a      | A = 1, B = 2                  | Solo `P2` envía valor 6 | `(A == 1)`                          | ✅ Sí     | —                          | Única guarda verdadera requiere `P3`, que no envió |
| b      | A = 0, B = 2                  | Solo `P2` envía valor 8 | `(A == 0)`                          | ❌ No     | 10 (8 + 2)                 | Ejecuta rama de `P2`, suma 2 a valor recibido     |
| c      | A = 2, B = 0                  | Solo `P3` envía valor 6 | `(B == 0)`                          | ❌ No     | 13 (6 + 7)                 | Ejecuta rama de `P3`, suma 7 al valor recibido    |
| d      | A = 2, B = 1                  | Solo `P3` envía valor 9 | —                                   | ❌ No     | -1                         | Ninguna guarda se cumple, `aux` no se modifica   |
| e      | A = 1, B = 0                  | Solo `P3` envía valor 14| `(A == 1)` y `(B == 0)`             | ❌ No     | 19 o 21                   | No determinismo entre 2 ramas (`+5` o `+7`)       |
| f      | A = 0, B = 0                  | `P2` envía 5, `P3` 9    | `(A == 0)` y `(B == 0)`             | ❌ No     | 7 o 16                    | No determinismo entre `P2` (`+2`) y `P3` (`+7`)   |


</details>

---

## 8) ¿Que valores quedan? 2

Dado el siguiente programa concurrente con memoria compartida, y suponiendo que todas las variables están inicializadas en 0 al empezar el programa y las instrucciones NO son atómicas. Para cada una de las opciones indique verdadero o falso.

**En caso de ser verdadero indique el camino de ejecución para llegar a ese valor, y en caso de ser falso justifique claramente su respuesta.**

<table><tr><td>P1</td><td>P2</td><td>P3</td></tr>
<tr><td>

```cpp
if (x = 0) then
    y := 4 * x + 2;
    x := y + 2 + x;
```
</td><td>

```cpp
if (x ≥ 0) then
    x := x + 1;
```
</td><td>

```cpp
x := x * 8 + x * 2 + 1;
```
</td></tr></table>


<details><summary>Detalles</summary>

```pascal
// Variables iniciales
x := 0;        // Valor inicial compartido por todos los procesos
y := 0;        // Solo P1 modifica y
```

Proceso P1 (con comentarios)

```pascal
if (x = 0) then        // P1 solo entra si x sigue valiendo 0
    y := 4 * x + 2;    // y se actualiza según el valor actual de x
    x := y + 2 + x;    // x se actualiza según el valor de y y el x que haya en ese momento
```

🔍 **P1 puede producir estos valores de `x`:**
- Si `x = 0`:  
  → `y = 4 * 0 + 2 = 2`  
  → `x = 2 + 2 + 0 = 4`

📌 **P1 solo puede dejar `x = 4`** como máximo si ejecuta completo y nadie interfiere.

🔷 Proceso P2

```pascal
if (x ≥ 0) then        // Siempre entra, porque x ≥ 0 al inicio
    x := x + 1;        // Suma 1 al valor actual de x
```

🔍 Si P2 se ejecuta después de P1:
- `x = 4 + 1 = 5`

🔶 Proceso P3

```pascal
x := x * 8 + x * 2 + 1;    // Esto equivale a x := 10 * x + 1
```

🔍 El valor de `x` que deja P3 depende directamente del valor que tenía x antes:
- Si `x = 1` → `x = 10 * 1 + 1 = 11`
- Si `x = 2` → `x = 10 * 2 + 1 = 21`
- Si `x = 5` → `x = 10 * 5 + 1 = 51`
- Si `x = 0` → `x = 1`

</details>


<details><summary><strong>a) El valor de x al terminar el programa es 9.</strong></summary>

🔎 Probamos combinaciones buscando `x = 9`

❌ Caso 1: P1 completo → P2 → P3

```pascal
// P1 ejecuta completo:
x = 0 → entra al if
y = 4*0 + 2 = 2
x = y + 2 + x = 2 + 2 + 0 = 4

// P2 ejecuta:
x = 4 + 1 = 5

// P3 ejecuta:
x = 10 * 5 + 1 = 51 → ❌ no es 9
```


❌ Caso 2: P2 → P3

```pascal
// P2 ejecuta:
x = 0 + 1 = 1

// P3 ejecuta:
x = 10 * 1 + 1 = 11 → ❌
```

❌ Caso 3: P3 → P2

```pascal
// P3 ejecuta:
x = 10 * 0 + 1 = 1

// P2 ejecuta:
x = 1 + 1 = 2 → ❌
```

❌ Caso 4: P3 con x = 2

```pascal
// Supongamos que x llega a 2 por P2 → P2
x = 0 + 1 = 1
x = 1 + 1 = 2

// P3 ejecuta:
x = 10 * 2 + 1 = 21 → ❌
```

❌ Conclusión del inciso **a)**

> ✅ **x = 9 no se puede alcanzar**, porque:
- P1 produce como mucho x = 4
- P2 suma 1 cada vez
- P3 hace `x = 10 * x + 1`, lo cual **siempre da un número impar mayor** (nunca 9)

---

✅ **Respuesta final del inciso a)**:  
**FALSO** – No existe ninguna secuencia de ejecución posible que lleve a `x = 9`.

</details>

<details><summary><strong>b) El valor de x al terminar el programa es 6.</strong></summary>

✔️ **Verdadero**

Una posible traza:

1. P1 ejecuta parcialmente: `y := 4 * 0 + 2 = 2`
2. P3 ejecuta: `x := 0 * 8 + 0 * 2 + 1 = 1`
3. P2 ejecuta: `x := 1 + 1 = 2`
4. P1 finaliza: `x := y + 2 + x = 2 + 2 + 2 = 6`

> Por lo tanto, **es posible** llegar a `x = 6`.

</details>

<details><summary><strong>c) El valor de x al terminar el programa es 11.</strong></summary>

✔️ **Verdadero**

Una traza simple:

1. P2 ejecuta: `x := 1`
2. P3 ejecuta: `x := 10 * 1 + 1 = 11`

> P1 no entra porque `x ≠ 0`.  
> Resultado final: `x = 11` → **válido**.
</details>

<details><summary><strong>d) Y siempre termina con alguno de los siguientes valores: 10, 6, 2, 0.</strong></summary>

✔️ **Verdadero**

Análisis por casos:

- `y = 0`: si **P1 no ejecuta el cuerpo del `if`** (porque `x ≠ 0` al momento de evaluarlo)
- `y = 2`: si P1 ejecuta el `if` con `x = 0`, y aún no ha sido modificado
- `y = 6`: si `x = 1` al momento de ejecutar `y := 4 * x + 2`
- `y = 10`: si `x = 2` cuando se evalúa la asignación

> Como la asignación de `y` depende directamente del valor de `x`, que puede ser modificado por otros procesos antes de ejecutarla, **solo esos cuatro valores** son posibles.
</details>

---

## 9) La solución a un problema es paralelizada

Suponga que la solución a un problema es paralelizada sobre **p** procesadores de dos maneras diferentes.
- En un caso, el **speedup (S)** está regido por la función **S=p-1** y
- en el otro por la **función S=p/2**.

**¿Cuál de las dos soluciones se comportará más eficientemente al crecer la cantidad de procesadores? Justifique claramente.**

<details><summary>Respuesta</summary>


De las dos soluciones, la que tiene **speedup S = p - 1** se comporta de forma más eficiente a medida que crece el número de procesadores.

Esto se debe a que el speedup ideal es **S = p**, y:

**S = p - 1** crece casi linealmente y se acerca al ideal.  
**S = p / 2** crece más lentamente y siempre es la mitad del número de procesadores.

Si analizamos la **eficiencia**, que se define como:

**E = S / p**

Para el primer caso:

**E = (p - 1) / p**

Esta eficiencia tiende a 1 cuando p crece.

Para el segundo caso:

**E = (p / 2) / p = 1 / 2**

La eficiencia es constante e igual al 50%, sin importar cuántos procesadores haya.

Por lo tanto, la solución con **S = p - 1** es más eficiente, ya que utiliza mejor los procesadores disponibles.


| Procesadores `p` | Speedup (S = p − 1) | Eficiencia (E = (p−1)/p) | Speedup (S = p / 2) | Eficiencia (E = 1/2) |
|------------------|----------------------|---------------------------|----------------------|----------------------|
| 2                | 1                    | 0.50                      | 1                    | 0.50                 |
| 4                | 3                    | 0.75                      | 2                    | 0.50                 |
| 8                | 7                    | 0.875                     | 4                    | 0.50                 |
| 16               | 15                   | 0.9375                    | 8                    | 0.50                 |
| 32               | 31                   | 0.96875                   | 16                   | 0.50                 |
| 64               | 63                   | 0.984375                  | 32                   | 0.50                 |
| 128              | 127                  | 0.9921875                 | 64                   | 0.50                 |

Conclusión

- La solución con **S = p - 1** **se vuelve cada vez más eficiente**, acercándose a un uso ideal de los recursos.
- La solución con **S = p / 2** **se estanca en el 50% de eficiencia**, sin importar cuánto aumente `p`.

</details>

Ahora suponga **S = 1/p** y **S = 1/p^2**



<details><summary>Respuesta</summary>

![alt text](/images/image-25.png)


**📋 Comparación entre S = 1/p y S = 1/(p^2)**

| Procesadores `p` | Speedup (S = 1/p) | Eficiencia (E = 1/p^2) | Speedup (S = 1/p^2) | Eficiencia (E = 1/p^3) |
|------------------|-------------------|-------------------------|----------------------|-------------------------|
| 1                | 1.00              | 1.00                    | 1.00                 | 1.00                    |
| 2                | 0.50              | 0.25                    | 0.25                 | 0.125                   |
| 4                | 0.25              | 0.0625                  | 0.0625               | 0.0156                  |
| 8                | 0.125             | 0.0156                  | 0.0156               | 0.0020                  |
| 16               | 0.0625            | 0.0039                  | 0.0039               | 0.00024                 |

✅ Conclusión:

- Ambos speedups disminuyen con más procesadores (son inversamente proporcionales).
- Pero **S = 1/p** siempre es mayor que **S = 1/(p^2)**.
- Lo mismo ocurre con la eficiencia: **1/(p^2)** decrece más lento que **1/(p^3)**.
- Por eso, **la solución con S = 1/p es más eficiente y escala mejor**.


</details>

---

## 10) La solución a un problema es paralelizada 2

Suponga que la solución a un problema es paralelizada sobre p procesadores de dos maneras diferentes. 
- En un caso, el **speedup (S)** está regido por la **función S=p/3**
- y en el otro por la función **S=p-3**.

**¿Cuál de las dos soluciones se comportará más eficientemente al crecer la cantidad de procesadores? Justifique claramente.**

**Suponiendo el uso de 5 procesadores:**

<details><summary>Respuesta</summary>

**Ejemplo con p = 5:**

- Opción 1: S = 5 / 3 ≈ 1.66  
- Opción 2: S = 5 − 3 = 2

En este caso, la segunda opción es más eficiente porque alcanza un mayor speedup.

**Comparación general:**

Ambas funciones son lineales, pero:

- S = p − 3 tiene una pendiente de 1  
- S = p / 3 tiene una pendiente de 1/3

Por lo tanto, **S = p − 3 crece más rápidamente** y se acerca más al ideal S = p a medida que p crece. También su eficiencia (E = S / p) tiende a 1 con el crecimiento de p, mientras que la eficiencia de S = p / 3 se mantiene constante en 1/3.

**Conclusión:**

La solución con **S = p − 3** se comporta mejor para valores grandes de `p`, ya que:

- Su speedup es mayor  
- Su eficiencia se aproxima a 1  
- Aprovecha mejor el uso de los procesadores

</details>

**Ahora, incrementamos la cantidad de procesadores suponemos 100 procesadores:**

<details><summary>Respuesta</summary>

- Solución 1 => S=100/3=33,33
- Solución 2 => S=100-3=97

Podemos decir, que a medida que **p** tiende a infinito, para la **solución 1** siempre el Speedup será la tercera parte en cambio para la **solución 2** el valor **"-3"** se vuelve despreciable.

Por lo tanto la **solución 2** es la que se comporta más eficientemente al crecer la cantidad de procesadores.

</details>

---

## 11) La solución a un problema es paralelizada 3

Suponga que la solución a un problema es paralelizada sobre **p** procesadores de dos maneras diferentes. 

- En un caso, el **speedup(s)** esta regido por la **función S = p-4**
- y el otro por la función **S = p/3** para **p > 4**.

**¿Cuál de las dos soluciones se comportara más eficientemente al crecer la cantidad de procesadores?**

<details><summary>Respuesta</summary>

A medida que crece la cantidad de procesadores, la solución cuyo speedup es **S = p − 4** se comportará de forma más eficiente que la de **S = p / 3**.

Esto se debe a que **S = p − 4** crece linealmente con pendiente 1, mientras que **S = p / 3** también crece linealmente pero con pendiente 1/3. Por lo tanto, la primera función se acerca más al speedup ideal **S = p**, aprovechando mejor los recursos disponibles.

Además, si analizamos la eficiencia **E = S / p**:

- En el primer caso:  
  **E = (p − 4) / p** → tiende a 1 cuando p crece  
- En el segundo caso:  
  **E = (p / 3) / p = 1/3** → eficiencia constante

**Conclusión:** La primera solución tiene mejor eficiencia y escalabilidad, especialmente cuando el número de procesadores es grande.


| Procesadores `p` | Speedup (p − 4) | Eficiencia (p−4)/p | Speedup (p / 3) | Eficiencia (1/3) |
|------------------|------------------|----------------------|------------------|------------------|
| 5                | 1                | 0.20                 | 1.67             | 0.33             |
| 8                | 4                | 0.50                 | 2.67             | 0.33             |
| 12               | 8                | 0.67                 | 4.00             | 0.33             |
| 20               | 16               | 0.80                 | 6.67             | 0.33             |
| 40               | 36               | 0.90                 | 13.33            | 0.33             |
| 100              | 96               | 0.96                 | 33.33            | 0.33             |


- A medida que `p` crece, la eficiencia de **S = p − 4** se acerca a 1 (ideal).
- La eficiencia de **S = p / 3** es constante y baja (0.33), sin importar el valor de `p`.
- Por eso, la función **S = p − 4** se comporta mucho mejor para valores grandes de `p`.

![alt text](/images/output.png)

</details>

---

## 12) La solución a un problema es paralelizada 4

Suponga que la solución a un problema es paralelizada sobre **p** procesadores de dos maneras diferentes.

- En un caso, la eficiencia está regido por la función **E = 1/p**
- y en el otro por la función **E =  1/p^2**.

**¿Cuál de las dos soluciones se comportará más eficientemente al crecer la cantidad de procesadores? Justifique.**

<details><summary>Respuesta</summary>

Claramente, a partir de p = 2, se observa que la eficiencia **E₁ = 1/p** es mayor que la eficiencia **E₂ = 1/p²**. Analicemos algunos valores:

- Para p = 1:  
  E₁ = 1/1 = 1  E₂ = 1/1 = 1  
- Para p = 2:  
  E₁ = 1/2 = 0.5  E₂ = 1/4 = 0.25  
- Para p = 3:  
  E₁ = 1/3 ≈ 0.33  E₂ = 1/9 ≈ 0.11  

Como se puede apreciar, **E₁ siempre es mayor que E₂** a partir de p = 2, y ambas eficiencias decrecen al aumentar el número de procesadores.


**Conclusión:**  
La solución con **E = 1/p** se comporta más eficientemente que la de **E = 1/p²**, ya que decrece más lentamente. Sin embargo, **ninguna de las dos escala bien** cuando `p` crece mucho, ya que ambas tienden a eficiencia cero.

![alt text](/images/output_1.png)

| Procesadores (p) | E1 = 1/p | E2 = 1/p² |
|------------------|----------|-----------|
| 1                | 1.0000   | 1.0000    |
| 2                | 0.5000   | 0.2500    |
| 3                | 0.3333   | 0.1111    |
| 4                | 0.2500   | 0.0625    |
| 5                | 0.2000   | 0.0400    |
| 10               | 0.1000   | 0.0100    |
| 20               | 0.0500   | 0.0025    |
| 50               | 0.0200   | 0.0004    |
| 100              | 0.0100   | 0.0001    |


</details>

---

## 13) Suponga que el tiempo de ejecución de un algoritmo Secuencial


Suponga que el tiempo de ejecución de un algoritmo secuencial es de **1000 unidades** de tiempo, de las cuales el **80%** corresponden a código paralelizable.

**¿Cuál es el límite en la mejora que puede obtenerse paralelizando el algoritmo?**

<details><summary>Respuesta</summary>

**🧠 ¿Qué estamos analizando?**

Tenemos un programa que tarda **1000 unidades de tiempo** si lo ejecutás de forma secuencial (en un solo procesador). Pero sabemos que **una parte se puede paralelizar** (hacer en varios procesadores a la vez) y otra parte no.

Nos dicen que:

- **80% del programa es paralelizable** → eso son 800 unidades de tiempo.  
- **20% es secuencial** → eso son 200 unidades de tiempo.  

**📌 ¿Qué pasa si usamos muchos procesadores?**

La **Ley de Amdahl** nos dice que **el tiempo total con paralelismo** va a ser:

```
T_paralelo = tiempo_secuencial + tiempo_paralelizable / cantidad_de_procesadores
```

Entonces, por ejemplo, si usamos **800 procesadores**, el cálculo sería:

```
T_paralelo = 200 + 800 / 800 = 200 + 1 = 201
```

Y el **speedup** (la mejora respecto del tiempo original) es:

```
Speedup = T_secuencial / T_paralelo = 1000 / 201 ≈ 4.97
```

Es decir, aunque pongas 1000, 2000 o más procesadores… **no podés bajar más de ese tiempo**, porque **las 200 unidades de código secuencial no se pueden paralelizar**. Esa es la **barrera natural** que impone la Ley de Amdahl.

**📉 ¿Por qué no conviene usar demasiados procesadores?**

Supongamos que usás 800 procesadores. Como el código secuencial tarda 200 unidades y **solo uno lo puede ejecutar**, **los otros 799 van a estar esperando**.

Por eso, conviene usar una **cantidad más chica** de procesadores que puedan estar trabajando todo el tiempo. Por ejemplo, con 5 procesadores:

```
T_paralelo = 200 + (800 / 5) = 200 + 160 = 360
Speedup = 1000 / 360 ≈ 2.78
```

No es el máximo speedup, pero **se aprovechan todos los procesadores** (menos desperdicio).

**✅ Conclusión**

- El **límite de mejora** está en ≈ 5 veces más rápido. No se puede mejorar más, por más procesadores que agregues.
- Si usás **muchos procesadores**, muchos van a estar **ociosos**.
- Lo mejor es **balancear**: usar la menor cantidad de procesadores que te dé una mejora sin que los demás queden esperando.

</details>

---

## 14) Suponga que el tiempo de ejecución de un algoritmo Secuencial 2

Suponga que el tiempo de ejecución de un algoritmo secuencial es de **8000 unidades** de tiempo, de las cuales solo el **90% corresponde a código paralelizable**.

**¿Cuál es el límite en la mejora que puede obtenerse paralelizando el algoritmo? Justifique.**

<details><summary>Respuesta</summary>


Sabemos que:
- **T_total = 8000**
- **90% es paralelizable → T_par = 7200**
- **10% es secuencial → T_sec = 800**

**📌 ¿Cuál es el mejor caso posible?**

El mejor caso se da si usamos **tantos procesadores como para que la parte paralela tarde solo 1 unidad de tiempo** (es decir, **7200 procesadores** para 7200 unidades paralelas).

Entonces, el **tiempo total mínimo** que podríamos lograr es:

```
T_mejor = T_sec + T_par / procesadores
T_mejor = 800 + 7200 / 7200
T_mejor = 800 + 1 = 801
```

⚡ Cálculo del speedup máximo (límite de mejora)

```
Speedup = T_secuencial / T_mejor
Speedup = 8000 / 801 ≈ 9.99
```

El **límite teórico de mejora** es aproximadamente **10 veces más rápido**.  
Esto se alinea con la **Ley de Amdahl**, que dice que el código secuencial limita la mejora total.

</details>

---

## 15) Suponga que el tiempo de ejecución de un algoritmo Secuencial 3

Suponga que el tiempo de ejecución de un algoritmo secuencial es de **10000 unidades** de tiempo, de las cuales **95% corresponden a código paralelizable**.

**¿Cuál es el límite en la mejora que puede obtenerse paralelinzado el algoritmo?**

<details><summary>Respuesta</summary>

El límite de mejora se alcanza cuando se utilizan **9500 procesadores** (uno por cada unidad de tiempo paralelizable), lo que reduce el tiempo de ejecución de la parte paralela a **1 unidad de tiempo**.  
La parte secuencial, que **no puede paralelizarse**, tarda **500 unidades de tiempo**.

Por lo tanto, el **tiempo total mínimo (T<sub>paralelo</sub>)** será:

```
Tparalelo = Tsecuencial + Tparalelizable / procesadores
Tparalelo = 500 + 1 = 501
```

El **speedup máximo** (mejora) se calcula como:

```
Speedup = Tsecuencial_total / Tparalelo = 10000 / 501 ≈ 19.96
```

> Esto significa que, incluso si seguimos agregando procesadores, **el máximo speedup que se puede lograr es aproximadamente 20**.

Este resultado **confirma la Ley de Amdahl**, la cual establece que el límite de paralelización de un algoritmo **no depende de cuántos procesadores se usen**, sino de **cuánta parte del código es secuencial**.

</details>

---

## 16) Calcular la suma de todos los valores

Suponga que **N** procesos poseen inicialmente cada uno un valor. Se debe calcular la suma de todos los valores y al finalizar la computación todos deben conocer dicha suma.

Analice (desde el punto de vista del número de mensajes y la performance global) las soluciones posibles con memoria distribuida para **arquitecturas en Estrella** (centralizada), **Anillo Circular**, **Totalmente Conectada** y **Árbol**.

<details><summary>arquitecturas en Estrella(centralizada)</summary>

En este tipo de arquitectura todos los procesos (workers) envían su valor local al procesador central (coordinador), este suma los `N` datos y reenvía la información de la suma al resto de los procesos.  
Por lo tanto se ejecutan `2(N-1)` mensajes. Si el procesador central dispone de una primitiva broadcast, se reduce a `N` mensajes.

En cuanto a la performance global, los mensajes al coordinador se envían casi al mismo tiempo.  
Estos se quedarán esperando hasta que el coordinador termine de computar la suma y envíe el resultado a todos.

```c
chan valor(INT);
resultados[n](INT suma);

Process P[0]{              // coordinador, v está inicializado
    INT v; INT sum = 0;
    sum = sum + v;
    for (i = 1 to n-1){
        receive valor(v);
        sum = sum + v;
    }
    for (i = 1 to n-1)
        send resultado[i](sum);
}

process P[i = 1 to n-1]{   // worker, v está inicializado
    INT v; INT sum;
    send valor(v);
    receive resultado[i](sum);
}
```

🧩 Supuestos

De nuevo usamos `n = 4` procesos:

| Proceso | Rol        | Valor local `v[i]` |
|---------|------------|--------------------|
| P[0]    | Coordinador| 2                  |
| P[1]    | Worker     | 3                  |
| P[2]    | Worker     | 5                  |
| P[3]    | Worker     | 7                  |

🎯 Objetivo

- `P[0]` recibe los valores de todos los procesos.
- Suma: `2 + 3 + 5 + 7 = 17`.
- Luego envía la **suma global** de vuelta a todos los workers.

🚀 Ejecución paso a paso

📨 Fase 1: Envío de los valores al coordinador

| Paso | Acción |
|------|--------|
| 1 | `P[1]` envía `3` a `P[0]` |
| 2 | `P[2]` envía `5` a `P[0]` |
| 3 | `P[3]` envía `7` a `P[0]` |
| 4 | `P[0]` ya tiene su `v = 2`, recibe `3`, `5`, y `7`, suma total = **17** |

📤 Fase 2: Coordinador difunde la suma

| Paso | Acción |
|------|--------|
| 5 | `P[0]` envía `17` a `P[1]` |
| 6 | `P[0]` envía `17` a `P[2]` |
| 7 | `P[0]` envía `17` a `P[3]` |

✅ Resultado final

| Proceso | Valor final conocido |
|---------|----------------------|
| P[0]    | 17 (lo calculó)      |
| P[1]    | 17 (lo recibió)      |
| P[2]    | 17 (lo recibió)      |
| P[3]    | 17 (lo recibió)      |

💬 Observaciones

- Total de mensajes: `2(n - 1)` = `2(4 - 1)` = **6 mensajes**
- Con **broadcast**: solo `n = 4` mensajes (1 de cada worker al coordinador, 1 broadcast de vuelta).
- Buena performance en tiempo, porque los workers **envían todos al mismo tiempo**.
- Pérdida de paralelismo en el cómputo: solo el **coordinador trabaja**, los demás esperan.
- **Punto único de falla**: si `P[0]` se cae, el sistema no funciona.

</details>

<details><summary>Anillo circular</summary>

Se tiene un anillo donde `P[i]` recibe mensajes de `P[i-1]` y envía mensajes a `P[i+1]`. `P[n-1]` tiene como sucesor a `P[0]`. El primer proceso envía su valor local ya que es el único que conoce.

Este esquema consta de dos etapas:

1. Cada proceso recibe un valor y lo suma con su valor local, transmitiendo la suma local a su sucesor.  
2. Todos reciben la suma global.

`P[0]` debe ser algo diferente para poder “arrancar” el procesamiento: debe enviar su valor local ya que es el único que conoce. Se requerirán **2(n-1)** mensajes.

A diferencia de la solución centralizada, esta reduce los requerimientos de memoria por proceso pero tardara más en ejecutarse, por más que el número de mensajes requeridos sea el mismo. Esto se debe a que cada proceso debe esperar un valor para computar una suma parcial y luego enviársela al siguiente proceso; es decir, un proceso trabaja por vez, se pierde el paralelismo.


```c
chan valor[n](suma);

process p[0] {
    INT v;
    INT suma = v;
    send valor[1](suma);
    receive valor[0](suma);
    send valor[1](suma);
}

process p[i = 1 to n-1] {
    INT v;
    INT suma;
    receive valor[i](suma);
    suma = suma + v;
    send valor[(i + 1) mod n](suma);
    receive valor[i](suma);
    if (i < n - 1)
        send valor[i + 1](suma);
}
```

| Proceso | `v[i]` |
|---------|--------|
| P[0]    | 2      |
| P[1]    | 3      |
| P[2]    | 5      |
| P[3]    | 7      |

El objetivo es que **todos los procesos conozcan la suma total**, que es `2 + 3 + 5 + 7 = 17`.

🧠 Etapa 1: **Suma parcial hacia adelante**

| Paso | Acción |
|------|--------|
| 1 | `P[0]` envía `2` a `P[1]` |
| 2 | `P[1]` recibe `2`, suma su `v=3`, total = `5`, envía `5` a `P[2]` |
| 3 | `P[2]` recibe `5`, suma su `v=5`, total = `10`, envía `10` a `P[3]` |
| 4 | `P[3]` recibe `10`, suma su `v=7`, total = `17`, envía `17` a `P[0]` |


🧠 Etapa 2: **Difusión de la suma global**

| Paso | Acción |
|------|--------|
| 5 | `P[0]` recibe `17` de `P[3]`, reenvía `17` a `P[1]` |
| 6 | `P[1]` recibe `17`, reenvía `17` a `P[2]` |
| 7 | `P[2]` recibe `17`, reenvía `17` a `P[3]` |
| 8 | `P[3]` recibe `17` |

✅ Resultado final

Todos los procesos conocen el valor total `17`.

| Proceso | Valor recibido |
|---------|----------------|
| P[0]    | 17             |
| P[1]    | 17             |
| P[2]    | 17             |
| P[3]    | 17             |

💬 Observaciones

- **Cantidad de mensajes**: 2(n - 1) = 2(4 - 1) = 6 mensajes, como indica tu descripción.
- **Secuencialidad**: cada proceso espera su turno para sumar → **no hay paralelismo**.
- **P[0]** es especial, porque inicia la suma **y también** es el primero que difunde la suma global.

</details>

<details><summary>Totalmente conectada (simetrica)</summary>

Todos los procesos ejecutan el mismo algoritmo. Existe un canal entre cada par de procesos.  
Cada uno transmite su dato local `v` a los `n-1` restantes. Luego recibe y procesa los `n-1` datos que le faltan, de modo que en paralelo toda la arquitectura está calculando la suma total y tiene acceso a los `n` datos.

Se ejecutan `n(n-1)` mensajes. Si se dispone de una primitiva de broadcast, serán `n` mensajes.  
Es la solución más corta y sencilla de programar, pero utiliza el mayor número de mensajes si no hay broadcast.

```cpp
chan valor[n](INT);

process p[i=0 to n-1] {
    INT v;
    INT nuevo, suma = v;
    
    for (k=0 to n-1 st k <> i)
        send valor[k](v);
        
    for (k=0 to n-1 st k <> i) {
        receive valor[i](nuevo);
        suma = suma + nuevo;
    }
}
```

🧩 Supuestos

Usamos de nuevo `n = 4` procesos y valores locales:

| Proceso | `v[i]` |
|---------|--------|
| P[0]    | 2      |
| P[1]    | 3      |
| P[2]    | 5      |
| P[3]    | 7      |

🚀 ¿Qué hace cada proceso?

- Cada proceso envía su valor a los otros 3 (`n-1`).
- Luego, **recibe** los 3 valores que le faltan, y los **suma**.
- Esto se hace en paralelo, es decir, todos los procesos trabajan al mismo tiempo.

📊 Ejecución paso a paso

**Fase 1: Envío**

| Proceso | Envía a...             | Mensajes |
|---------|------------------------|----------|
| P[0]    | P[1], P[2], P[3]       | 3        |
| P[1]    | P[0], P[2], P[3]       | 3        |
| P[2]    | P[0], P[1], P[3]       | 3        |
| P[3]    | P[0], P[1], P[2]       | 3        |
| **Total** |                        | **12 mensajes** |

**Fase 2: Recepción y suma**

Cada proceso recibe 3 valores y los suma con el propio:

| Proceso | Valores recibidos | Suma final |
|---------|-------------------|------------|
| P[0]    | 3, 5, 7           | 2 + 3 + 5 + 7 = 17 |
| P[1]    | 2, 5, 7           | 3 + 2 + 5 + 7 = 17 |
| P[2]    | 2, 3, 7           | 5 + 2 + 3 + 7 = 17 |
| P[3]    | 2, 3, 5           | 7 + 2 + 3 + 5 = 17 |

✅ Resultado final

Todos conocen la suma global **17**.

| Proceso | Suma calculada |
|---------|----------------|
| P[0]    | 17             |
| P[1]    | 17             |
| P[2]    | 17             |
| P[3]    | 17             |

💬 Observaciones

- Total de mensajes: `n(n-1)` = `4 × 3` = **12 mensajes**
- Todos trabajan en **paralelo** → **alta velocidad**
- Pero: requiere **muchos canales y mensajes**
- Si tuvieras broadcast, solo necesitarías **n mensajes** (1 por proceso).

</details>

<details><summary>Arbol</summary>

Se tiene una red de procesadores (nodos) conectados por canales de comunicación bidireccionales. Cada nodo se comunica directamente con sus vecinos. Si un nodo quiere enviar un mensaje a toda la red, debería construir un árbol de expansión de la misma, poniéndose a él mismo como raíz.

El nodo raíz envía un mensaje por broadcast a todos los hijos, junto con el árbol construido. Cada nodo examina el árbol recibido para determinar los hijos a los cuales deben reenviar el mensaje, y así sucesivamente.

Se envían `n - 1` mensajes, uno por cada padre/hijo del árbol.


🧩 Supuestos

- Tenemos `n = 7` nodos numerados del `0` al `6`.
- Se construye un **árbol de expansión** para propagar un mensaje, con el **nodo `0` como raíz**.
- El árbol tiene esta estructura (por simplicidad):

```
        0
      / | \
     1  2  3
        |   \
        4    5
              \
               6
```

---

🎯 Objetivo

Difundir un **mensaje** desde el nodo raíz (`0`) hacia todos los demás nodos usando el árbol.

 🚀 Ejecución paso a paso

| Paso | Nodo emisor | Nodo receptor | Descripción |
|------|-------------|----------------|-------------|
| 1    | 0           | 1              | Nodo 0 envía a su hijo 1 |
| 2    | 0           | 2              | Nodo 0 envía a su hijo 2 |
| 3    | 0           | 3              | Nodo 0 envía a su hijo 3 |
| 4    | 2           | 4              | Nodo 2 reenvía a su hijo 4 |
| 5    | 3           | 5              | Nodo 3 reenvía a su hijo 5 |
| 6    | 5           | 6              | Nodo 5 reenvía a su hijo 6 |

✅ Resultado final

Todos los nodos reciben el mensaje, usando solo `n - 1 = 6` mensajes.

| Nodo | ¿Recibió el mensaje? |
|------|------------------------|
| 0    | Sí (es la raíz)       |
| 1    | Sí                    |
| 2    | Sí                    |
| 3    | Sí                    |
| 4    | Sí                    |
| 5    | Sí                    |
| 6    | Sí                    |

💬 Observaciones

- **Mensajes totales**: `n - 1 = 6`
- Es la forma más eficiente si ya tenemos el árbol.
- Permite **paralelismo**: varios nodos pueden reenviar a la vez.
- Ideal para redes distribuidas con **vecindades limitadas** (no totalmente conectadas).
- Si se necesita hacer una suma global, se puede hacer un **recorrido postorden** (bottom-up), y luego **difundir el resultado** (top-down).

</details>

---

## 17) Token passing con mensajes asincrónicos

Implemente una solución al problema de exclusión mutua distribuida entre **N** procesos utilizado un algoritmo de tipo token passing con mensajes asincrónicos.

<details><summary>Respuesta</summary>

El algoritmo de **token passing**, se basa en un tipo especial de mensaje o **“token”** que
puede utilizarse para otorgar un **permiso** (control) o para **recoger información global** de la arquitectura distribuida.

Si **User[1:n]** son un conjunto de procesos de aplicación que contienen secciones críticas y
no críticas. Hay que desarrollar los protocolos de interacción (E/S a las secciones críticas),
asegurando **exclusión mútua**, **no deadlock**, **evitar demoras innecesarias** y **eventualmente fairness**.

Para no ocupar los procesos **User** en el manejo de los **tokens**, ideamos un proceso **auxiliar (helper)** por cada **User**, de modo de manejar la circulación de los **tokens**. Cuando **helper[i]** tiene el **token** adecuado, significa que **User[i]** tendrá prioridad para acceder a la sección crítica.


```cpp
chan token[n]() ;                   # para envío de tokens
chan enter[n](), go[n](), exit[n](); # para comunicación proceso-helper

process helper[i = 1..N] {
    while(true){
        receive token[i]();               # recibe el token
        if(!(empty(enter[i]))){          # si su proceso quiere usar la SC
            receive enter[i]();
            send go[i]();                # le da permiso y lo espera a que termine
            receive exit[i]();
        }
        send token[i MOD N + 1]();       # y lo envía al siguiente cíclicamente
    }
}

process user[i = 1..N] {
    while(true){
        send enter[i]();
        receive go[i]();
        ... sección crítica ...
        send exit[i]();
        ... sección no crítica ...
    }
}
```

> Se asume que el primero ya tenga el token

</details>

---

# 📢 Miralas de Reojo

<div align="center">
<img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExbXU3c3h4NHh2anBkb3I2NWt4dDZxN2lsNjU0YnBtNWh6Y2UyaXI5dCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/pb2NDIcPTwNpu/giphy.gif" width="500px">
</div>

---

## 1) Propuesta al problema de alocación SJN

**Sea la siguiente solución propuesta al problema de alocación SJN (Short Job Next):**

```nginx
Monitor SJN {
    Bool libre = true;
    Cond turno;

    Procedure request {
        If (not libre) wait (turno, tiempo);
        Libre = false;
    }

    Procedure release {
        Libre = true;
        Signal (turno);
    }
}
```

**a) ¿Funciona correctamente con disciplina de señalización Signal and continue? Justifique.**

<details><summary>👀 Respuesta</summary>


No, la solución no funciona correctamente con la disciplina de señalización **Signal and Continue (S&C)**.

Bajo esta disciplina, cuando un proceso realiza un `signal`, **continúa ejecutando dentro del monitor**, y el proceso que fue despertado es enviado a la **cola de listos (ready queue)** del sistema operativo. Esto implica que su reingreso al monitor depende de la **política de planificación del sistema**, y no se garantiza que sea el próximo en ejecutarse.

En consecuencia, un proceso con menor tiempo (según la política **Shortest Job Next**) podría quedar **retrasado** si otro proceso ingresa antes al monitor. Por lo tanto, el orden de ejecución no refleja necesariamente la prioridad establecida por el parámetro `tiempo`, y **no se cumple el objetivo del SJN**.

**Respuesta de un random**

> Con S&C un proceso que es despertado para poder seguir ejecutando es pasado a la cola
> de ready en cuyo caso su orden de ejecución depende de la política que se utilice para
> ordenar los procesos en dicha cola. Puede ser que sea retrasado en esa cola permitiendo
> que otro proceso ejecute en el monitor antes que el por lo que podría no cumplirse el
> objetivo del SJN.

![alt text](/images/image-2.png)

</details>

****b)** ¿Funciona correctamente con disciplina de señalización *signal and wait*? Justifique.**

<details><summary>👀 Respuesta</summary>

Sí, **la solución funciona correctamente** con la disciplina de señalización **Signal and Wait (S&W)**.

En esta disciplina, cuando un proceso ejecuta un `signal`, **cede inmediatamente el control del monitor** al proceso que fue despertado, el cual **continúa su ejecución justo después del `wait`**. El proceso que hizo el `signal` pasa a la cola de listos y debe esperar su turno para volver a ingresar al monitor.

Esto garantiza que el proceso con menor tiempo (según la política Shortest Job Next) —que estaba esperando con prioridad— **será efectivamente el próximo en acceder al recurso**, evitando que otro proceso pueda adelantarse y violar el orden deseado.

Por lo tanto, **la política SJN se respeta correctamente bajo Signal and Wait**, ya que se mantiene el control sobre el orden de ejecución de los procesos en espera.


📘 **Definiciones complementarias:**

- **Signal and Continue:** El proceso que ejecuta el `signal` **continúa usando el monitor**, mientras que el proceso despertado **debe competir** por reingresar al monitor.
- **Signal and Wait:** El proceso que ejecuta el `signal` **cede el monitor** al proceso despertado, que continúa su ejecución **justo después del `wait`**.


</details>


<details><summary>📊 Comparación entre <strong>Signal and Continue</strong> vs <strong>Signal and Wait en SJN</strong></summary>


| **Aspecto**                         | **Signal and Continue (S&C)**                                                                 | **Signal and Wait (S&W)**                                                                   |
|-------------------------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| **¿Quién sigue ejecutando en el monitor después del `signal`?** | El proceso que hizo el `signal` continúa.                                                     | El proceso que fue despertado entra inmediatamente al monitor.                              |
| **Estado del proceso despertado**   | Pasa a la **cola de listos** y debe competir por reingresar al monitor.                       | **Continúa inmediatamente** dentro del monitor (no compite por el acceso).                  |
| **Riesgo de pérdida de prioridad (SJN)** | **Alto**: otro proceso puede ingresar antes que el de menor tiempo.                          | **Nulo**: se garantiza que el proceso con menor tiempo accede primero.                      |
| **¿Se respeta la política SJN?**    | ❌ **No**: puede no ejecutarse el proceso con menor tiempo debido a la competencia externa.   | ✅ **Sí**: el proceso con menor tiempo es el próximo en continuar.                          |
| **Uso recomendado en SJN**          | No recomendado, ya que puede romper la prioridad por tiempo.                                  | Recomendado, ya que respeta el orden de espera basado en el tiempo.                         |
| **Control de acceso**               | Depende del planificador del sistema operativo.                                               | Controlado directamente por el monitor y su lógica de sincronización.                      |

</details>

---

## 2) “passing the condition” En Semaforos

**Utilice la técnica de “passing the condition” para implementar un semáforo *fair* usando monitores.**

<details><summary>Codigo</summary>

```cpp
monitor Semaforo {
    int s = 1, espera = 0;
    cond pos;

    procedure P() {
        if (s == 0) {
            espera++;
            wait(pos);
        } else {
            s = s - 1;
        }
    };

    procedure V() {
        if (espera == 0) {
            s = s + 1;
        } else {
            espera--;
            signal(pos);
        }
    };
};
```
</details>

---

## 3) Problema de Concurrencia

Sea **“ocupados”** una variable entera inicializada en **N** que representa la cantidad de **slots** ocupados de un **buffer**, y sean **P1** y **P2** dos programas que se ejecutan de manera concurrente, donde cada una de las instrucciones que los componen son atómicas.

<table><tr><td>P1</td><td>P2</td></tr><tr><td>

```cpp
if (ocupados < N) then
begin
    buffer := elemento_a_agregar;
    ocupados := ocupados + 1;
end;
```
</td><td>

```cpp
if (ocupados > 0) then
begin
    ocupados := ocupados - 1;
    elemento_a_sacar := buffer;
end;
```
</td></tr></table>

**¿El programa funciona correctamente para asegurar el manejo del buffer?**
- Si su respuesta es afirmativa justifique.
- Sino, encuentre una secuencia de ejecución que lo verifique y escríbala, y además modifique la solución para que funcione correctamente (Suponga buffer, elemento_a_agregar y elemento_a_sacar variables declaradas).

<details><summary>Respuesta</summary>

**No, el programa no funciona correctamente en un entorno concurrente.**

🔍 Justificación con secuencia de ejecución:

Supongamos que el buffer está **lleno** (`ocupados = N`). En ese momento:

1. El proceso **P2** evalúa `if (ocupados > 0)`, lo cual es **verdadero**.
2. Luego, **P2 ejecuta `ocupados := ocupados - 1`**, pero **aún no ha leído el dato del buffer**.
3. Justo después, el proceso **P1** evalúa su condición `if (ocupados < N)`, que **ahora también es verdadera**, ya que P2 lo acaba de decrementar.
4. Entonces, **P1 escribe en el buffer un nuevo valor**, sobrescribiendo el dato que **P2 todavía no alcanzó a leer**.

⚠️ Como resultado, **P2 pierde el dato original** y lee un valor nuevo que **no era el que debía consumir**. Esto genera una **condición de carrera** (race condition) y un **error de sincronización**.


✅ Solución propuesta:

Para evitar este problema, es necesario **postergar el decremento de `ocupados` en P2 hasta después de leer el valor del buffer**, asegurando que el dato se consuma correctamente antes de liberar el espacio.

✔️ Código corregido de P2

```pascal
if (ocupados > 0) then
begin
    elemento_a_sacar := buffer;
    ocupados := ocupados - 1;
end;
```

Con esta corrección, **P1 no podrá ingresar** hasta que **P2 haya terminado de leer** el valor, manteniendo la coherencia del estado del buffer.


🧠 Nota adicional:

Este tipo de errores son comunes cuando no se usa un mecanismo de sincronización explícito, como **semáforos, monitores o exclusión mutua**. En un sistema real, lo ideal sería proteger el acceso al buffer con algún tipo de **región crítica** o control de concurrencia.

</details>

---

## 4) Problema de Concurrencia 2

Sea **“cantidad”** una variable entera inicializada en 0 que representa la cantidad de
elementos de un **buffer**, y sean **P1** y **P2** dos programas que se ejecutan de manera concurrente, donde cada una de las instrucciones que los componen son atómicas.

<table><tr><td>P1</td><td>P2</td></tr><tr><td>

```cpp
if (cantidad = 0) then
begin
    cantidad := cantidad + 1;
    buffer := elemento_a_agregar;
end;
```
</td><td>

```cpp
if (cantidad > 0) then
begin
    elemento_a_sacar := buffer;
    cantidad := cantidad - 1;
end;
```
</td></tr></table>


Además existen dos alumnos de concurrente que analizan el programa y opinan lo siguiente:

- **“Pepe**: este programa funciona correctamente ya que las instrucciones son atómicas”.
- “**José**: no Pepe estás equivocado, hay por lo menos una secuencia de ejecución en
la cual funciona erróneamente”

¿Con cuál de los dos alumnos está de acuerdo? Si está de acuerdo con Pepe justifique su respuesta.
Si está de acuerdo con José encuentre una secuencia de ejecución que verifique lo que José opina y escríbala, y modifique la solución para que funcione correctamente (Suponga buffer y elemento variables declaradas). (22-04-2009)

<details><summary>Resultado</summary>


✅ **Estoy de acuerdo con José.**

Aunque las instrucciones sean atómicas, el programa **no es seguro concurrentemente**, ya que existen **interleavings (intercalaciones de ejecución)** posibles que generan un comportamiento incorrecto.

🔍 **Ejemplo de secuencia de ejecución errónea:**

1. El proceso **P1** evalúa la condición `if (cantidad = 0)` → **verdadera**, y entra al `begin`.
2. **P1 ejecuta la instrucción `cantidad := cantidad + 1`**, pero **aún no ha escrito en el buffer**.
3. En ese momento, el proceso **P1 se interrumpe**, y **P2 toma el control**.
4. **P2 evalúa `if (cantidad > 0)`** → **verdadera** (porque `cantidad` ahora vale 1).
5. **P2 ejecuta `elemento_a_sacar := buffer`**, pero **el buffer aún no fue actualizado por P1**.
6. Como resultado, **P2 lee un valor inválido o desactualizado** del buffer.


⚠️ **Problema identificado:**

> El hecho de que las instrucciones sean atómicas **no garantiza la atomicidad de toda la sección crítica** compuesta por múltiples instrucciones relacionadas entre sí.


✅ **Modificación para que funcione correctamente:**

Una forma de corregirlo es **reordenar las instrucciones de P1**, asegurando que el valor se escriba en el buffer **antes de habilitar su lectura** (es decir, antes de incrementar `cantidad`):

```pascal
// P1 corregido:
if (cantidad = 0) then
begin
    buffer := elemento_a_agregar;
    cantidad := cantidad + 1;
end;
```

De este modo, si **P2 observa que `cantidad > 0`**, entonces es seguro asumir que el buffer **ya contiene un valor válido** para ser consumido.

**🧠 Conclusión:**

Estoy de acuerdo con **José**, porque:
- El código original permite que **P2 lea un valor inválido** si se interrumpe a P1 en el momento inadecuado.
- La solución requiere **ajustar el orden de operaciones** para garantizar consistencia en el acceso al buffer, incluso si cada instrucción individual es atómica.

</details>

---

## 5) Indique los posibles valores finales de x

**Indique los posibles valores finales de x en el siguiente programa (justifique claramente su respuesta):**

```c
int x = 3;
sem s1 = 1, s2 = 0;

co
  // P1
  P(s1);              // Espera mutex
  x = x * x;          
  V(s1);              // Libera mutex

  // P2
  P(s2);              // Espera señal de P3
  P(s1);              // Espera mutex
  x = x * 3;
  V(s1);

  // P3
  P(s1);              // Espera mutex
  x = x - 2;
  V(s2);              // Señaliza a P2
  V(s1);
oc
```

**s1 →** *mutex:* puede pasar un solo proceso por vez.  
**s2 →** *semáforo de señalización:* esperan señalización de un evento y pasa sólo uno.

> Aunque se libere un semaforo, no tiene que volver a ejecutarse ya que no estamos en un while (Si un semaforo paso PASO)

<details><summary>Respuesta</summary>

| Orden de ejecución       | Valor final de `x` |
|--------------------------|--------------------|
| P1 → P3 → P2             | 21                 |
| P3 → P2 → P1             | 9                  |
| P3 → P1 → P2             | 3                  |

**P1** y **P3** comienzan esperando a **s1**. Por ser un mutex, sólo puede continuar uno de ellos y no será interrumpido por el otro hasta liberar a **s1**.

**Primer resultado**

Si comienza P1: 
- Asigna x=9
- luego incrementa **s1** permitiendo que continúe **P3**.
- **P3** asigna **x=7** y señala **s2**.
- Esto habilita a **P2** que estaba esperando.
- Si **P2** continúa, intentará obtener s1 con lo cual se vuelve a bloquear volviendo el control a **P3**.
- En cualquier caso, **P3** libera a **s1** y termina.
- **P2** es despertado, asigna x = 21 y termina.
- Valor **final x=21.**

**Segundo y Tercer resultado**

Si comienza **P3**:

- Asigna **x = 1** y señala a **s2**.
- Esto habilita a **P2** que estaba esperando.
- Si P2 continúa, intentará obtener **s1** con lo cual se vuelve a bloquear volviendo el control a **P3**.
- Cuando **P3** libera a **s1**, **P1** y **P2** pueden competir por él:
    - **Si gana P1**: 
        - asigna **x=1**,
        - libera a **s1** y termina; 
        - finaliza **P2** y asigna **x = 3**.
        - **Valor final x=3.**
    - **Si gana P2**:
        - asigna **x=3**,
        - libera a **s1** y termina;
        - finaliza **P1** y asigna **x = 9**.
        - Valor final **x = 9**.

**P2** nunca puede comenzar la historia ya que espera un semáforo de señalización que sólo **P3** señala. Cualquier historia en la que **P2** esté antes de **P3** es inválida. En todas las historias los semáforos terminan con los mismos valores con los que están inicializados.

</details>

---

## 6) Cuales valores de k son posibles

**c)** Dado el siguiente programa concurrente indique cuáles valores de `K` son posibles al finalizar, y describa una secuencia de instrucciones para obtener dicho resultado:

```cpp
Process P1 {
    for (i = 1 to K) {
        N = N + 1;
    }
}

Process P2 {
    for (i = 1 to K) {
        N = N + 1;
    }
}
```

i) 2K
ii) 2K + 2  
iii) K  
iv) 2 

<details><summary>Respuesta</summary>

```c
// Ambos procesos ejecutan el mismo bucle:
for (i = 1 to K)
    N = N + 1;
```

✅ **i) Valor final = 2K**  
**Caso posible:** ejecución secuencial sin interferencia.

**Ejemplo (K = 3):**

```
P1: N=0 -> 1 -> 2 -> 3
P2: N=3 -> 4 -> 5 -> 6
Resultado final: N = 6 = 2*K
```


❌ **ii) Valor final = 2K + 2**  
**Caso imposible.**

**Justificación:**  
Cada proceso ejecuta exactamente `K` incrementos. Como mucho se pueden hacer `2K` sumas. No hay forma de hacer más sin ejecutar más iteraciones, lo cual no ocurre.

✅ **iii) Valor final = K**  
**Caso posible:** interferencia total entre procesos. Se pisan las operaciones.

**Ejemplo (K = 3):**

```
N inicialmente = 0

Intercalado:
P1 lee N=0       // aún no actualiza
P2 lee N=0       // aún no actualiza
P1 escribe N=1
P2 escribe N=1   // pisa el valor anterior → se pierde un incremento

Repite este patrón durante las 3 iteraciones.

Resultado final: solo 3 incrementos efectivos → N = 3 = K
```

✅ **iv) Valor final = 2**  
**Caso posible:** interferencia total y mal intercalado extremo.

**Ejemplo (K = 3):**

```
N = 0

P1 iteración 1: lee N=0
P2 iteración 1: lee N=0
P1 escribe N=1
P2 escribe N=1   → pisa a P1

P1 iteración 2: lee N=1
P2 iteración 2: lee N=1
P1 escribe N=2
P2 escribe N=2   → pisa a P1

Resultado final: N = 2
```

</details>

---

# 🚨 Rezar para que no Tomen

<div align="center">
<img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExODNrODc5OWpvdTgwNzhtMDZ2b2dnNXZnMHhtZmVlOHRrbmo5ang3ZyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l0HlNcdK4NM0vt4yI/giphy.gif" width="500px">
</div>

---

## 1) Resuelva con monitores

Resuelva con monitores el siguiente problema:  
Tres clases de procesos comparten el acceso a una lista enlazada: **searchers**, **inserters** y **deleters**.

- Los **searchers** sólo examinan la lista, y por lo tanto pueden ejecutar concurrentemente unos con otros.  
- Los **inserters** agregan nuevos ítems al final de la lista; las inserciones deben ser mutuamente exclusivas para evitar insertar dos ítems casi al mismo tiempo. Sin embargo, un insert puede hacerse en paralelo con uno o más searchers.  
- Por último, los **deleters** remueven ítems de cualquier lugar de la lista. A lo sumo un deleter puede acceder la lista a la vez, y el borrado también debe ser mutuamente exclusivo con **searchers** e **inserters**.

<details><summary>Codigo</summary>

```cpp
monitor Controlador_ListaEnlazada {
    int numSearchers = 0, numInserters = 0, numDeleters = 0;
    cond searchers, inserters, deleters;

    procedure pedir_Deleter() {
        while (numSearchers > 0 OR numInserters > 0 OR numDeleters > 0) {
            wait(deleters);
        }
        numDeleters = numDeleters + 1;
    }

    procedure liberar_Deleter() {
        numDeleters = numDeleters - 1;
        signal(inserters);
        signal(deleters);
        signal_all(searchers);
    }

    procedure pedir_Searcher() {
        while (numDeleters > 0) {
            wait(searchers);
        }
        numSearchers = numSearchers + 1;
    }

    procedure liberar_Searcher() {
        numSearchers = numSearchers - 1;
        if (numSearchers == 0 AND numInserters == 0) {
            signal(deleters);
        }
    }

    procedure pedir_Inserter() {
        while (numDeleters > 0 OR numInserters > 0) {
            wait(inserters);
        }
        numInserters = numInserters + 1;
    }

    procedure liberar_Inserter() {
        numInserters = numInserters - 1;
        signal(inserters);
        if (numSearchers == 0) {
            signal(deleters);
        }
    }
}
```

🧵 Procesos:

```cpp
process Searchers[i = 1..S] {
    Controlador_ListaEnlazada.pedir_Searcher();
    <Realiza búsqueda en la lista>
    Controlador_ListaEnlazada.liberar_Searcher();
}

process Inserters[j = 1..I] {
    Controlador_ListaEnlazada.pedir_Inserter();
    <Inserta en la lista>
    Controlador_ListaEnlazada.liberar_Inserter();
}

process Deleters[k = 1..D] {
    Controlador_ListaEnlazada.pedir_Deleter();
    <Borra en la lista>
    Controlador_ListaEnlazada.liberar_Deleter();
}
```

🧠 **Resumen: Monitor `Controlador_ListaEnlazada`**

👥 Tipos de procesos:
- **Searchers**: pueden acceder **concurrentemente**, salvo que haya un **Deleter**.
- **Inserters**: acceden **de a uno**, pero **pueden convivir con Searchers**.
- **Deleters**: requieren **exclusión total** (no pueden ejecutarse junto a ningún otro proceso).


🔒 Comportamiento de sincronización:
- `Searchers` esperan si hay un `Deleter`.
- `Inserters` esperan si hay otro `Inserter` o un `Deleter`.
- `Deleters` esperan si hay cualquier otro proceso activo (Searcher o Inserter).
- Al liberar, se despiertan procesos bloqueados según condiciones.

✅ ¿Funciona correctamente?
Sí, **el monitor implementa correctamente las restricciones** de sincronización para los tres tipos de procesos.   Asegura exclusión mutua, convivencia segura y respeta la lógica de prioridades.

</details>

---

## 2) Protocolos de Acceso a la SC

En los protocolos de acceso a sección crítica vistos en clase, cada proceso ejecuta el mismo algoritmo. Una manera alternativa de resolver el problema es usando un proceso **coordinador**. En este caso, cuando cada proceso **SC[i]** quiere entrar a su **sección crítica** le avisa al **coordinador**, y espera a que éste le dé permiso. Al terminar de ejecutar su sección crítica, el proceso **SC[i]** le avisa al **coordinador**.  

Desarrolle protocolos para los procesos **SC[i]** y el **coordinador** usando sólo variables compartidas (no tenga en cuenta la propiedad de eventual entrada).

<details><summary>Respuesta</summary>

```cpp
int aviso[1:N] = ([N] 0), permiso[1:N] = ([N] 0);
```

<table><td>

```cpp
process SC[i = 1 to N] {
    SNC;

    // Protocolo de entrada
    permiso[i] = 1;
    while (aviso[i] == 0) skip;

    // Sección crítica
    SC;

    // Protocolo de salida
    aviso[i] = 0;
    SNC;
}
```
</td><td>

```cpp
process Coordinador {
    int i = 1;
    while (true) {
        // Espera que algún proceso solicite permiso
        while (permiso[i] == 0)
            i = i mod N + 1;

        // Otorga permiso al proceso i
        permiso[i] = 0;
        aviso[i] = 1;

        // Espera a que el proceso libere la SC
        while (aviso[i] == 1) skip;
    }
}
```
</td></table>

</details>

---

## 3) Solución a la Criba

> 💀 Dudo mucho que tomen este ejercicio, lo pongo por las dudas

Describa la solución utilizando la criba de Eratóstenes al problema de hallar los primos entre 2 y n. **¿Cómo termina el algoritmo? ¿Qué modificaría para que no termine de esa manera?**

<details><summary>Codigo</summary>

La criba de Eratóstenes es un algoritmo clásico para determinar cuáles números en un rango son primos. Supongamos que queremos generar todos los primos entre **2** y **n**. Primero, escribimos una lista con todos los números:

```
2 3 4 5 6 7 ... n
```

Comenzando con el primer número no tachado en la lista, 2, recorremos la lista y borramos los múltiplos de ese número. Si n es impar, obtenemos la lista:

```
2 3 5 7 ... n
```

En este momento, los números borrados no son primos; los números que quedan todavía son candidatos a ser primos. Pasamos al próximo número, **3**, y repetimos el anterior proceso borrando los **múltiplos de 3**. Si seguimos este proceso hasta que todo número fue considerado, los números que quedan en la lista final serán todos los primos entre **2** y **n**.

Para solucionar este problema de forma paralela podemos emplear un pipeline de procesos filtro.

- Cada filtro recibe una serie de números de su predecesor y envía una serie de números a su sucesor.
- El primer número que recibe un filtro es el próximo primo más grande;
- Le pasa a su sucesor todos los números que no son múltiplos del primero.

El siguiente es el algoritmo pipeline para la generación de números primos.

Por cada canal, el primer número es primo y todos los otros números no son múltiplo de ningún primo menor que el primer número:

```cpp
Process Criba[1]
{
    int p = 2;

    for [i = 3 to n by 2] 
        Criba[2] ! (i);
}

Process Criba[i = 2 to L]
{
    int p, proximo;

    Criba[i-1] ? p;
    do Criba[i-1] ? (proximo) →
        if ((proximo MOD p) <> 0) →
            Criba[i+1] ! (proximo);
        fi
    od
}
```

- El primer proceso, **Criba[1]**, envía todos los números impares desde `3 a n` a **Criba[2]**.
- Cada uno de los otros procesos recibe una serie de números de su predecesor.
- El primer número **`p`** que recibe el proceso **`Criba[i]`** es el **i-ésimo** primo.
- Cada Criba[i] subsecuentemente pasa todos los otros números que recibe que no son múltiplos de su primo **`p`**.
- El número total **`L`** de procesos Cribe debe ser lo suficientemente grande para garantizar que todos los primos hasta **`n`** son generados. Por ejemplo, hay 25 primos menores que 100;
- el porcentaje decrece para valores crecientes de **`n`**.

El programa anterior termina en deadlock, ya que no hay forma de saber cuál es el último número de la secuencia y cada proceso queda esperando un próximo número que no llega.

Podemos fácilmente modificarlo para que termine normalmente usando centinelas, es decir que al final de los streams de entrada son marcados por un centinela

```cpp
# EOS: End Of Stream (-1 indica fin del flujo)

Process Criba[1] {
    int p = 2;

    # Enviar todos los números impares desde 3 hasta n a Criba[2]
    for [i = 3 to n by 2]
        Criba[2] ! i;

    # Enviar fin de flujo
    Criba[2] ! -1;
}

Process Criba[i = 2 to L] {
    int p, proximo;
    boolean seguir = true;

    # Recibe el primer número (primo)
    Criba[i-1] ? p;

    do (seguir);
        # Recibe siguiente candidato
        Criba[i-1] ? proximo ->

        if (proximo = -1) {
            seguir = false;
            Criba[i+1] ! -1;   # Propaga EOS al siguiente proceso
        }
        else if ((proximo MOD p) <> 0) {
            Criba[i+1] ! proximo;  # Si no es múltiplo, lo pasa
        }
    od
}
```

</details>


---

## 4) Transformar Solucion usando mensajes asincronicos


**Dada la siguiente solución con monitores al problema de alocación de un recurso con múltiples unidades, transforme la misma en una solución utilizando mensajes asincrónicos.**

```cpp
Monitor Alocador_Recurso {
    INT disponible = MAXUNIDADES;
    SET unidades = valores iniciales;
    COND libre;   // TRUE cuando hay recursos

    procedure adquirir(INT id) {
        if (disponible == 0)
            wait(libre);
        else {
            disponible = disponible - 1;
            remove(unidades, id);
        }
    }

    procedure liberar(INT id) {
        insert(unidades, id);
        if (empty(libre))
            disponible := disponible + 1;
        else
            signal(libre);
    }
}
```

<details><summary>Respuesta</summary>

```cpp
type clase_op = enum(adquirir, liberar);
chan request(int idCliente, claseOp oper, int idUnidad);
chan respuesta[n](int id_unidad);

Process Administrador_Recurso {
    int disponible = MAXUNIDADES;
    set unidades = valor inicial disponible;
    queue pendientes;

    while (true) {
        receive request(idCliente, oper, id_unidad);

        if (oper == adquirir) {
            if (disponible > 0) {
                disponible = disponible - 1;
                remove(unidades, id_unidad);
                send respuesta[idCliente](id_unidad);
            } else {
                insert(pendientes, idCliente);
            }
        } else {
            if (empty(pendientes)) {
                disponible = disponible + 1;
                insert(unidades, id_unidad);
            } else {
                remove(pendientes, idCliente);
                send respuesta[idCliente](id_unidad);
            }
        }
    }
}
// Fin del proceso Administrador_Recurso

Process Cliente[i = 1 to n] {
    int id_unidad;

    send request(i, adquirir, 0);
    receive respuesta[i](id_unidad);

    // Usa la unidad

    send request(i, liberar, id_unidad);
}
```

***🧠 1. **Modelo de comunicación*****

- **Monitores** utilizan una **comunicación directa** entre procesos a través de **procedimientos compartidos**. El proceso cliente **entra al monitor**, ejecuta `adquirir()` o `liberar()`, y **bloquea su ejecución** si no puede continuar (por ejemplo, si no hay recursos).
  
- **Mensajes asincrónicos**, en cambio, se basan en **comunicación por paso de mensajes**. El cliente **envía un mensaje** al administrador (`request`) y luego **espera la respuesta** por otro canal (`respuesta[i]`). No hay acceso directo a las variables compartidas; todo se coordina mediante mensajes.

**🔁 2. **Sincronización y control de acceso****

- En el **monitor**, la sincronización es **implícita**: si `disponible == 0`, el proceso ejecuta `wait(libre)` y queda **suspendido automáticamente** hasta que otro proceso haga `signal(libre)` al liberar un recurso.

- En la versión **con mensajes**, no hay suspensión automática. El administrador debe **mantener una cola de espera (`pendientes`)** y decidir manualmente a quién responder y cuándo. Si alguien libera una unidad y hay clientes esperando, el administrador **desencola** y **responde explícitamente**.

**🔐 3. **Visibilidad y consistencia del estado****

- En el monitor, los procesos tienen **acceso directo a las variables** `disponible`, `unidades`, etc., pero solo **uno a la vez**, garantizando exclusión mutua.

- Con mensajes asincrónicos, **solo el administrador** conoce y modifica el estado global. Los clientes **no ven directamente cuántos recursos quedan**; solo saben si obtuvieron uno o no, cuando reciben la respuesta.

**🧩 4. **Modelo de espera****

- En monitores, la espera se maneja con `wait` y `signal`, que pueden funcionar según dos disciplinas:  
  - **Signal and Wait** (el proceso que señala cede el monitor al despertado)  
  - **Signal and Continue** (el proceso que señala continúa)

- En mensajes, **la espera es activa y manual**: el cliente **se bloquea esperando una respuesta**, y el administrador debe tener lógica para enviarle esa respuesta **cuando le toque**.

**⚙️ 5. **Aplicabilidad según arquitectura****

- Los **monitores** son más adecuados para sistemas **centralizados o con memoria compartida**, ya que dependen de sincronización interna y acceso directo a variables.

- Los **mensajes asincrónicos** son ideales en **sistemas distribuidos o clusters**, donde no existe memoria compartida y cada proceso corre en su propio nodo. Permiten **separar cómputo y comunicación** y escalar fácilmente.

**💬 Ejemplo concreto**

Supongamos que hay 3 unidades disponibles, y 5 procesos piden recursos.

- En el **monitor**, los 3 primeros entran y adquieren recursos; los otros 2 quedan bloqueados con `wait(libre)` hasta que alguien libere. Luego, `liberar()` hace `signal()` y despierta a uno.

- En la **versión con mensajes**, los 3 primeros reciben respuesta del administrador inmediatamente. Los otros 2 son **enviados a la cola `pendientes`**, y recién serán atendidos cuando un recurso sea liberado y el administrador procese esa cola.

**✅ Conclusión**

- El uso de **monitores** es más directo y automatizado, pero menos flexible fuera de sistemas con memoria compartida.
- El enfoque de **mensajes asincrónicos** permite mayor **control y distribución**, pero requiere manejar manualmente colas, lógica de respuesta y sincronización, lo cual lo hace más complejo pero también más escalable.


</details>

---


## 5) Problema de ordenar de menor a mayor un arreglo

Sea el problema de ordenar de menor a mayor un arreglo de A[1..n]

<details><summary><strong>1. Escriba un programa donde dos procesos (cada uno con n/2 valores) realicen la operación en paralelo mediante una serie de intercambios.</strong></summary>

<table><td>

```cpp
Process P1
{
    int nuevo, a1[1:n/2];
    const mayor = n/2;

    // ordenar a1 en orden no decreciente
    P2 ! (a1[mayor]);
    P2 ? (nuevo);

    do a1[mayor] > nuevo →
        // poner nuevo en el lugar correcto
        // en a1, descartando 
        // el viejo a1[mayor]
        P2 ! (a1[mayor]);
        P2 ? (nuevo);
    od
}
```
</td><td>

```cpp
Process P2
{
    int nuevo, a2[1:n/2];
    const menor = 1;

    // ordenar a2 en orden no decreciente
    P1 ? (nuevo);
    P1 ! (a2[menor]);

    do a2[menor] < nuevo →
        // poner nuevo en el lugar correcto
        // en a2, descartando
        // el viejo a2[menor]
        P1 ? (nuevo);
        P1 ! (a2[menor]);
    od
}
```

</td></table></details>

<details><summary><strong>2. ¿Cuántos mensajes intercambian en el mejor de los casos? ¿Y en el peor de los casos?</strong></summary>

**Mejor caso:**  
En el escenario más favorable, los arreglos ya están correctamente distribuidos:  
- Los `n/2` valores más pequeños están en el proceso **P1**.  
- Los `n/2` valores más grandes están en **P2**.

Como los extremos (mayor de `a1` y menor de `a2`) ya están en orden, los procesos solo necesitan hacer **una comparación inicial** y confirmar que no hay que intercambiar nada.  

**Resultado:** Solo se envían **2 mensajes**:  
- P1 envía su mayor a P2.  
- P2 responde con su menor a P1.

🧪 **Ejemplo con n = 6 (a1 y a2 de tamaño 3)**

Supongamos:
```text
P1: a1 = [1, 2, 3]     (valores más chicos)
P2: a2 = [4, 5, 6]     (valores más grandes)
```

- Proceso:
    - `1)` P1 envía el mayor de `a1`: `3`
    - `2)` P2 envía el menor de `a2`: `4`
    - `3)` P1 verifica: `3 < 4` ✅, así que **todo está ordenado**
- ✅ Resultado:
    - Se intercambian **2 mensajes**: `3 →`, `4 →`
    - **No se modifica nada**

---

**Peor caso:**

En el peor de los casos, todos los elementos están en el proceso equivocado:  
- Es decir, **los mayores están en P1** y **los menores en P2**.

Esto obligará a intercambiar completamente los `n/2` elementos entre ambos procesos.  
Cada valor necesita **un mensaje de ida y uno de vuelta**, ya que el intercambio es coordinado y requiere validación mutua.

**Resultado:** Se intercambian **`n` mensajes**:  
- `n/2` valores de P1 a P2  
- `n/2` valores de P2 a P1 → total: `(n/2) * 2 = n` mensajes


Supongamos:
```text
P1: a1 = [6, 5, 4]     (valores grandes, mal ubicados)
P2: a2 = [3, 2, 1]     (valores chicos, mal ubicados)
```

- Proceso:
    - P1 envía su mayor `6`, P2 su menor `1`
    - Ambos comparan y detectan que los elementos están desordenados, por lo tanto **empiezan a intercambiar valores** de uno en uno.
- Intercambios:
    - 1. `6` ↔ `1`
    - 2. `5` ↔ `2`
    - 3. `4` ↔ `3`

Cada par requiere **2 mensajes** (ida y vuelta).

✅ Resultado:
- Se hacen **3 intercambios**
- Se envían **6 mensajes (3 * 2)**


📊 Resumen final:

| Caso        | Cantidad de mensajes | Explicación breve                                       |
|-------------|----------------------|---------------------------------------------------------|
| Mejor caso  | 2                    | Solo se comparan los extremos, no se intercambia nada  |
| Peor caso   | n                    | Se intercambian todos los valores (n/2 * 2 = n)         |



</details>


**3. Utilice la idea de 1), extienda la solución a K procesos, con n/k valores c/u (“odd-even-exchange sort”).**

Asumimos que existen **n** procesos **P[1:n]** y que **n** es par. Cada proceso ejecuta una serie de rondas. En las rondas impares, los procesos impares **P[odd]** intercambian valores con el siguiente proceso impar **P[odd+1]** si el valor esta fuera de orden. En rondas pares, los procesos pares **P[even]** intercambia valores con el siguiente proceso par **P[even+1]** si los valores estan fuera de orden. **P[1]** y **P[n]** no hacen nada en las rondas pares.

<details><summary>Respuesta</summary>

```cpp
process Proc[i = 1..k] {
    int a[1..n/k];        // subarreglo local ordenado
    int dato;
    const min = 1;
    const max = n/k;

    ordenar_localmente(a);  // ordenar el arreglo local al iniciar

    for ronda = 1 to k {

        // Si la ronda y el índice tienen la misma paridad: proceso actúa como EMISOR
        if (i mod 2 == ronda mod 2 and i < k) {
            // Enviar el mayor valor local al vecino derecho
            send(proc[i+1], a[max]);
            receive(proc[i+1], dato);

            while (a[max] > dato) {
                // Insertar el dato recibido ordenadamente en 'a', descartando el mayor
                insertar_en_orden(a, dato);
                send(proc[i+1], a[max]);
                receive(proc[i+1], dato);
            }
        }

        // Si la ronda y el índice tienen distinta paridad: proceso actúa como RECEPTOR
        if (i mod 2 != ronda mod 2 and i > 1) {
            receive(proc[i-1], dato);
            send(proc[i-1], a[min]);

            while (a[min] < dato) {
                // Insertar el dato recibido ordenadamente en 'a', descartando el menor
                insertar_en_orden(a, dato);
                receive(proc[i-1], dato);
                send(proc[i-1], a[min]);
            }
        }
    }
}
```

> Lo de abajo no hace falta pero es para probar

**Con k = 4 procesos y n = 8 valores**, llevando las rondas hasta que los valores queden **totalmente ordenados globalmente**.

Configuración inicial

Cada proceso tiene 2 elementos (n/k = 2), ordenados localmente:

| Proceso | Valores iniciales |
|---------|-------------------|
| P1      | [8, 9]            |
| P2      | [5, 7]            |
| P3      | [3, 6]            |
| P4      | [1, 4]            |

Rondas del algoritmo (hasta que esté ordenado)

| Ronda | Procesos activos | Cambios realizados                                                                                         | Estado final por proceso                          |
|-------|------------------|------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| 0     | —                | —                                                                                                          | P1: [8, 9], P2: [5, 7], P3: [3, 6], P4: [1, 4]     |
| 1     | P1↔P2, P3↔P4     | P1⇄P2: 9⇄5 → P1: [5, 8], P2: [7, 9]<br>P3⇄P4: 6⇄1 → P3: [1, 3], P4: [4, 6]                                 | P1: [5, 8], P2: [7, 9], P3: [1, 3], P4: [4, 6]     |
| 2     | P2↔P3            | 9⇄1 → P2: [1, 7], P3: [3, 9]                                                                               | P1: [5, 8], P2: [1, 7], P3: [3, 9], P4: [4, 6]     |
| 3     | P1↔P2, P3↔P4     | 8⇄1 → P1: [1, 5], P2: [7, 8]; 9⇄4 → P3: [3, 4], P4: [6, 9]                                                  | P1: [1, 5], P2: [7, 8], P3: [3, 4], P4: [6, 9]     |
| 4     | P2↔P3            | 8⇄3 → P2: [3, 7], P3: [4, 8]                                                                               | P1: [1, 5], P2: [3, 7], P3: [4, 8], P4: [6, 9]     |
| 5     | P1↔P2, P3↔P4     | 5⇄3 → P1: [1, 3], P2: [5, 7]; 8⇄6 → P3: [4, 6], P4: [8, 9]                                                  | P1: [1, 3], P2: [5, 7], P3: [4, 6], P4: [8, 9]     |
| 6     | P2↔P3            | 7⇄4 → P2: [4, 5], P3: [6, 7]                                                                               | P1: [1, 3], P2: [4, 5], P3: [6, 7], P4: [8, 9]     |
| 7     | P1↔P2, P3↔P4     | No intercambios necesarios (valores ya ordenados)                                                          | P1: [1, 3], P2: [4, 5], P3: [6, 7], P4: [8, 9]     |


```
P1: [1, 3]
P2: [4, 5]
P3: [6, 7]
P4: [8, 9]
→ Resultado final: [1, 3, 4, 5, 6, 7, 8, 9]
```

El arreglo quedó completamente ordenado tras **7 rondas**, que coincide con el peor caso esperado (hasta k rondas).


</details>

**b. ¿Cuántos mensajes intercambian en 3) en el mejor caso? ¿Y en el peor de los casos?**

<details><summary>Respuesta</summary>

Si cada proceso ejecuta suficientes rondas para garantizar que la lista estará ordenada (en general, al menos **k** rondas), en el **k-proceso**, cada uno intercambia hasta **(n/k)+1** mensajes por ronda. El algoritmo requiere hasta **k^2** * **(n/k+1)**.

Se puede usar un proceso coordinador al cual todos los procesos le envían en cada ronda si realizaron algún cambio o no.

Si al recibir todos los mensajes el coordinador detecta que ninguno cambio nada les comunica que terminaron.

Esto agrega **overhead** de mensajes ya que se envían mensajes al coordinador y desde el coordinador. Con **n** procesos tenemos un overhead de **2*k** mensajes en cada ronda.

> Nota: Utilice un mecanismo de pasaje de mensajes, justifique la elección del mismo.

PMS es más adecuado en este caso porque los procesos deben sincronizar de a pares en cada ronda por lo que **PMA** no sería tan útil para la resolución de este problema ya que se necesitaría implementar una barrera simétrica para sincronizar los procesos de cada etapa.
</details>

---

## 6) Problema de ordenar de menor a mayor 2

Suponga los siguientes métodos de ordenación de menor a mayor para **n** valores (**n** par y potencia de 2), utilizando pasaje de mensajes:
- **1)** Un pipeline de filtros. El primero hace input de los valores de a uno por vez, mantiene el mínimo y le pasa los otros al siguiente. Cada filtro hace lo mismo: recibe un stream de valores desde el predecesor, mantiene el más chico y pasa los otros al sucesor.
- **2)** Una red de procesos filtro (como la de la figura).
    ![alt text](/images/image-8.png)
- **3)** Odd/even exchange sort. Hay **n** procesos **P[1:n]**, Cada uno ejecuta una serie de rondas. En las rondas **“impares”**, los procesos con número impar **P[impar]** intercambian valores con **P[impar+1]**. En las rondas **“pares”**, los procesos con número par **P[par]** intercambian valores con **P[par+1]** (**P[1]** y **P[n]** no hacen nada en las rondas **“pares”**). En cada caso, si los números están desordenados actualizan su valor con el recibido.


Asuma que cada proceso tiene almacenamiento local sólo para dos valores (el próximo y el mantenido hasta ese momento).

**a) ¿Cuántos procesos son necesarios en 1 y 2? Justifique.**

<details><summary>Respuesta</summary>


Para la alternativa del **pipeline de filtros**, se requieren **n procesos**, ya que cada uno actúa como un filtro que **retiene el valor mínimo** recibido hasta el momento y **envía los valores mayores** al siguiente. Como se desea ordenar `n` elementos y cada proceso retiene uno, se necesitan `n` procesos para que todos los valores queden almacenados, uno en cada proceso, en orden ascendente.

En cambio, para la alternativa de la **red de procesos filtro** (basada en una estructura de árbol binario), se necesitan **n - 1 procesos**. Esto se debe a que los valores iniciales están en las hojas del árbol (hay `n` hojas), y los nodos internos se encargan de ir fusionando pares de valores o secuencias. En un árbol binario completo con `n` hojas, hay exactamente `n - 1` nodos internos. Por lo tanto, se requieren `n - 1` procesos de merge para combinar todos los valores en una única secuencia ordenada.

Perfecto, Fabián. A continuación te doy **un ejemplo para cada alternativa** (pipeline de filtros y red de merges) con **n = 4 valores** (potencia de 2) y su **tabla de ejecución** correspondiente para que visualices cómo se comportan ambos métodos.

📌 Ejemplo 1: **Pipeline de filtros**

**Idea:** Cada proceso filtra el mínimo de los valores que recibe y pasa el resto al siguiente.

**Valores iniciales:** 6, 2, 8, 4 (se envían en ese orden)

**Estructura:**

```
Entrada → P1 → P2 → P3 → P4
```

**Tabla de ejecución**

| Paso | Valor recibido | P1       | P2       | P3       | P4       |
|------|----------------|----------|----------|----------|----------|
| 1    | 6              | 6        | —        | —        | —        |
| 2    | 2              | 2 (↓6)   | 6        | —        | —        |
| 3    | 8              | 2 (↓8)   | 6 (↓8)   | 8        | —        |
| 4    | 4              | 2 (↓4)   | 4 (↓6)   | 6 (↓8)   | 8        |

**Resultado final:**  
P1: 2  
P2: 4  
P3: 6  
P4: 8  
→ **[2, 4, 6, 8]** (ordenado)

**Procesos necesarios:** 4 (uno por cada valor)

📌 Ejemplo 2: **Red de merges (filtros)**

**Idea:** Se usan procesos que combinan pares de valores en orden. Cada proceso mergea dos entradas ordenadas y produce una salida ordenada.

**Valores iniciales (en hojas):**  
Entrada a M1: 6 y 2  
Entrada a M2: 8 y 4

**Estructura:**

```
Nivel 0:      6     2       8     4
               \   /         \   /
Nivel 1:         M1           M2
                  \         /
Nivel 2:             M3
```

**Tabla de ejecución**

| Merge | Entrada izq | Entrada der | Salida ordenada |
|-------|-------------|-------------|------------------|
| M1    | 6           | 2           | [2, 6]           |
| M2    | 8           | 4           | [4, 8]           |
| M3    | [2, 6]      | [4, 8]      | [2, 4, 6, 8]     |

**Procesos necesarios:**  
- 3 merges → **n − 1 = 3 procesos**

**📋 Comparación en tabla**

| Método               | Valores iniciales | Nº de procesos | Resultado final    | Observaciones                               |
|----------------------|-------------------|----------------|---------------------|---------------------------------------------|
| Pipeline de filtros  | 6, 2, 8, 4         | 4              | [2, 4, 6, 8]         | Cada proceso retiene uno; paso a paso       |
| Red de merges        | 6, 2, 8, 4         | 3              | [2, 4, 6, 8]         | Requiere mergear en árbol binario completo  |

</details>

**b) ¿Cuántos mensajes envía cada algoritmo para ordenar los valores? Justifique.**

<details><summary>Respuesta</summary>


📌 Pipeline

A cada proceso se le asigna un número del 1 al n, y los valores se envían uno por uno al primer proceso.

- **El proceso 1** recibe `n` valores, se queda con el menor y envía `n−1` al proceso 2.
- **El proceso 2** recibe `n−1` valores, se queda con el menor y envía `n−2` al proceso 3.
- ...
- **El proceso n** recibe 1 valor y no envía ninguno.

La cantidad total de mensajes enviados entre procesos es:

![alt text](/images/image-9.png)

A esto se le suman **n mensajes EOS** (End Of Stream), ya que cada proceso necesita saber cuándo detenerse. Por lo tanto:

![alt text](/images/image-10.png)

---

📌 Red de procesos filtro (merge tree)

En este caso, con `n` valores a ordenar y una red de `log₂(n)` niveles, la cantidad de mensajes de combinación es:

![alt text](/images/image-11.png)

Esto incluye las comparaciones y fusiones realizadas en cada nivel del árbol.

Además, se deben sumar:

- `n` mensajes para enviar los valores desde los nodos hoja (datos iniciales).
- `n − 1` mensajes EOS desde los nodos internos al superior para finalizar.

![alt text](/images/image-12.png)

---

📌 Odd/Even Exchange Sort

Si cada proceso ejecuta suficientes rondas para garantizar el orden (en general, hasta `k` rondas con `k` procesos), entonces en cada ronda cada proceso intercambia hasta:

![alt text](/images/image-13.png)

Cada intercambio requiere dos mensajes (ida y vuelta), y se repite durante `k` rondas, así que el total de mensajes es:

![alt text](/images/image-14.png)

Resumen de todos los resultados

![alt text](/images/image-15.png)

- En el **Pipeline**, cada proceso filtra y pasa el resto, por lo que la cantidad de mensajes crece cuadráticamente.
- En la **Red de filtros (árbol de merges)**, el ordenamiento sigue una estructura logarítmica. Muy eficiente para merges en paralelo.
- En el **Odd/Even**, el ordenamiento depende de la cantidad de rondas (`k`), y aunque es simple de implementar, puede requerir muchos mensajes si los datos están muy desordenados.

</details>

**c) ¿En cada caso, cuáles mensajes pueden ser enviados en paralelo (asumiendo que existe el hardware apropiado) y cuáles son enviados secuencialmente? Justifique.**

<details><summary>Respuesta</summary>

- **Pipeline de filtros:**  
  Una vez que el pipeline está lleno, es posible enviar mensajes en paralelo entre todos los procesos del pipeline. Cada proceso está recibiendo, procesando y enviando valores simultáneamente. Por lo tanto, en un instante dado, pueden enviarse en paralelo hasta `n` mensajes (uno por cada proceso). Al inicio y al final, el envío es más secuencial, pero en régimen estable, el flujo es completamente paralelo.

- **Red de procesos filtro (merge tree):**  
  En esta estructura, los mensajes pueden enviarse en paralelo **a nivel de cada capa del árbol**. Cada proceso del mismo nivel actúa de forma independiente, por lo que se pueden enviar hasta `n / 2`, `n / 4`, ..., `1` mensajes en paralelo según el nivel. El envío entre niveles debe ser secuencial (los procesos de un nivel deben esperar los resultados del anterior).

- **Odd/Even Exchange Sort:**  
  En cada ronda (par o impar), todos los procesos que participan pueden enviar mensajes en paralelo. Por ejemplo, en una ronda impar, todos los procesos con índice impar se comunican simultáneamente con sus vecinos. Por lo tanto, en cada ronda puede haber hasta `n/2` mensajes en paralelo.

**📋 Comparación: Paralelismo en el envío de mensajes**

| Método                   | Paralelismo posible                       | Secuencialidad obligatoria                        | Observaciones clave                                                  |
|--------------------------|--------------------------------------------|--------------------------------------------------|----------------------------------------------------------------------|
| **Pipeline de filtros**  | Hasta **n mensajes** por instante (una vez lleno) | Inicio (pipeline vacío) y último paso             | Cada proceso recibe, filtra y reenvía simultáneamente               |
| **Red de merges (filtros)** | Hasta **n / 2, n / 4, ..., 1** por nivel del árbol | Entre niveles del árbol                           | Dentro de un mismo nivel: procesos trabajan en paralelo             |
| **Odd/Even Exchange Sort** | Hasta **n / 2 mensajes** por ronda        | Rondas ejecutadas secuencialmente                 | En cada ronda, procesos con mismo tipo (par/impar) se comunican     |


</details>


**d) ¿Cuál es el tiempo total de ejecución de cada algoritmo? Asuma que cada operación de comparación o de envío de mensaje toma 1 una unidad de tiempo. Justifique.**

<details><summary>Respuesta</summary>

**📌 Algoritmo 1: **Pipeline de filtros****

Cada mensaje enviado implica una comparación y luego el envío (2 unidades de tiempo).

En el punto (a) se determinó que se envían

![alt text](/images/image-17.png)

Por lo tanto, el tiempo total es:

![alt text](/images/image-18.png)

Entonces:  

![alt text](/images/image-19.png)

**📌 Algoritmo 2: **Red de procesos filtro (árbol de merges)****

Cada mensaje también implica 1 comparación y 1 envío → 2 unidades por mensaje.

Ya vimos que se envían

![alt text](/images/image-20.png)

Entonces:

![alt text](/images/image-21.png)

**📌 Algoritmo 3: **Odd/Even Exchange Sort****

- En cada ronda, cada proceso:
  - Hace una comparación (1)
  - Envía un mensaje (1)
  - Recibe un mensaje (1)
  - Asigna/intercambia valores (1)  
  → Total = **4 unidades por proceso por ronda**
- En el peor caso, se necesitan hasta `n` rondas.
- Entonces:

![alt text](/images/image-22.png)

Acomodando la tabla final

![alt text](/images/image-23.png)

</details>

<details><summary>Tabla final</summary>

![alt text](/images/image-24.png)
</details>


---

## 7) Suponga que un proceso productor y `n` procesos consumidores

(Broadcast atómico). Suponga que un proceso productor y **n** procesos consumidores comparten un **buffer** unitario. El productor deposita mensajes en el buffer y los consumidores los retiran. Cada mensaje depositado por el productor tiene que ser retirado por los **n** consumidores antes de que el productor pueda depositar otro mensaje en el buffer.

<details><summary><strong>a) Desarrolle una solución utilizando semáforos.</strong></summary>

```cpp
sem depositar := 1;
sem retirar := 1;
sem consumi[n] := ([n] 0);
int cant_consumido := ([n] 0);
T buffer;

process productor {
    while (true) {
        P(depositar);
        buffer := generarDato();     // Devuelve un entero para el buffer
        cant_consumido := 0;
        for i to n do
            V(consumi[i]);
    }
}

process consumidor[i = 1..n] {
    T dato;
    while (true) {
        P(consumi[i]);              // Espero que el dato esté en el buffer
        P(retirar);                 // Espero para tener acceso al buffer
        dato := buffer;
        cant_consumido++;
        if (cant_consumido == n)
            V(depositar);
        V(retirar);
    }
}
```

🎯 Objetivo

> El **productor** debe generar un dato y colocarlo en un buffer compartido.  
> **Cada consumidor** debe leer ese dato **una única vez**.  
> **Solo cuando todos lo hayan leído**, el productor podrá colocar un nuevo dato.

🧩 Supuestos para el ejemplo

- Hay `n = 2` consumidores: `C1` y `C2`
- El buffer inicialmente está vacío
- El productor genera números enteros: `1`, `2`, `3`, etc.

🔄 Ejecución paso a paso

🔹 Estado inicial

| Variable         | Valor inicial |
|------------------|---------------|
| `depositar`      | 1             |
| `retirar`        | 1             |
| `consumi[1]`     | 0             |
| `consumi[2]`     | 0             |
| `cant_consumido` | 0             |
| `buffer`         | vacío         |

⏱ Paso 1: El productor genera un dato

1. `P(depositar)` → pasa (vale 1)
2. `buffer := generarDato() → 1`
3. `cant_consumido := 0`
4. `V(consumi[1])` → `consumi[1] = 1`
5. `V(consumi[2])` → `consumi[2] = 1`

🔁 El productor queda esperando a que los 2 consumidores consuman antes de generar otro dato.

⏱ Paso 2: El consumidor 1 consume

1. `P(consumi[1])` → pasa
2. `P(retirar)` → pasa (vale 1)
3. `dato := buffer = 1`
4. `cant_consumido := 1`
5. `cant_consumido != n → no hace nada`
6. `V(retirar)` → `retirar = 1`

⏱ Paso 3: El consumidor 2 consume

1. `P(consumi[2])` → pasa
2. `P(retirar)` → pasa
3. `dato := buffer = 1`
4. `cant_consumido := 2`
5. `cant_consumido == n` → entonces `V(depositar)` → ahora el productor puede seguir
6. `V(retirar)`

⏱ Paso 4: El productor continúa

1. `P(depositar)` → pasa (porque fue liberado)
2. `buffer := 2`
3. `cant_consumido := 0`
4. `V(consumi[1])`, `V(consumi[2])` → y sigue el ciclo

✅ Garantías del algoritmo

| Propiedad                    | Cumple |
|-----------------------------|--------|
| Exclusión mutua en acceso   | ✅     |
| Cada consumidor lee una vez | ✅     |
| Productor espera a todos     | ✅     |
| No hay pérdida de datos     | ✅     |

</details>

b) Suponga que el buffer tiene **b** slots. El productor puede depositar mensaje sólo en slots vacíos y cada mensaje tiene que ser recibido por los **n** consumidores antes de que el slot pueda ser reusado. Además, cada consumidor debe recibir los mensajes en el orden en que fueron depositados (note que los distintos consumidores pueden recibir los mensajes en distintos momentos siempre que los reciban en orden).

Extienda la respuesta dada en a) para resolver este problema más general.

<details><summary>Respuesta</summary>

```cpp
sem retirar[tamBuffer] := 1;              // semáforo para cada slot del buffer
sem consumir[n] := ([n] 0);
int cant_consumido[tamBuffer] := ([n] 0);
T buffer[tamBuffer];

process productor {
    int posLibre := 0;                   // Siguiente posición libre del buffer (productor)
    while(true){
        P(depositar);
        buffer[posLibre] := generarDato();     // Devuelve dato tipo T para el buffer
        cant_consumido[posLibre] := 0;
        for i to n do
            V(consumir[i]);
        posLibre := (posLibre + 1) mod n;
    }
}

process consumidor[i: 1..n] {
    int post_actual := 0;               // Slot del que debe consumir
    T dato;
    while(true){
        P(consumir[i]);
        P(retirar[post_actual]);        // Espera por un slot en particular
        dato := buffer[post_actual]; // El acceso de esta manera no se encuentra en la imagen pero supongo que esta bien
        cant_consumido[post_actual]++;
        if (cant_consumido[post_actual] == n)
            V(depositar);
        V(retirar[post_actual]);
        post_actual := (post_actual + 1) mod n;
    }
}
```

🧩 Supuestos del ejemplo

- `tamBuffer = 2` → hay dos slots: `buffer[0]` y `buffer[1]`
- `n = 2` → hay dos consumidores: `C1` y `C2`
- `buffer[i]` contiene datos generados por el productor
- Cada dato debe ser consumido por ambos consumidores **antes de poder sobrescribir el slot**
- Los consumidores deben leer los datos en orden

🔁 Estado inicial

| Variable / Recurso          | Valor inicial        |
|----------------------------|----------------------|
| `buffer`                   | [_, _]               |
| `cant_consumido[0]`        | 0                    |
| `cant_consumido[1]`        | 0                    |
| `retirar[0]`, `retirar[1]` | 1                    |
| `consumir[1]`, `consumir[2]` | 0 (esperando dato) |
| `posLibre` (productor)     | 0                    |
| `post_actual` (consumidores)| 0                    |

⏱ Paso 1: El productor genera el primer dato

1. `P(depositar)` → OK
2. `buffer[0] := generarDato() → 10`
3. `cant_consumido[0] := 0`
4. `V(consumir[1])`, `V(consumir[2])`
5. `posLibre := 1` (próximo slot)

⏱ Paso 2: Ambos consumidores empiezan a consumir `buffer[0]` (dato 10)

Consumer 1:
1. `P(consumir[1])`
2. `P(retirar[0])` → OK
3. `dato := buffer[0] → 10`
4. `cant_consumido[0] := 1`
5. `V(retirar[0])` (libera acceso al slot)
6. `post_actual := 1`

Consumer 2:
1. `P(consumir[2])`
2. `P(retirar[0])` → OK
3. `dato := buffer[0] → 10`
4. `cant_consumido[0] := 2`
5. `cant_consumido[0] == n` → `V(depositar)` → libera al productor
6. `V(retirar[0])`
7. `post_actual := 1`

⏱ Paso 3: El productor genera el segundo dato

1. `P(depositar)` → OK (fue liberado)
2. `buffer[1] := generarDato() → 20`
3. `cant_consumido[1] := 0`
4. `V(consumir[1])`, `V(consumir[2])`
5. `posLibre := 0`

⏱ Paso 4: Ambos consumidores consumen `buffer[1]` (dato 20)

Consumer 1:
1. `P(consumir[1])`
2. `P(retirar[1])`
3. `dato := buffer[1] → 20`
4. `cant_consumido[1] := 1`
5. `V(retirar[1])`
6. `post_actual := 0`

Consumer 2:
1. `P(consumir[2])`
2. `P(retirar[1])`
3. `dato := buffer[1] → 20`
4. `cant_consumido[1] := 2`
5. `V(depositar)` (productor puede continuar)
6. `V(retirar[1])`
7. `post_actual := 0`

🔁 Y así continúa el ciclo...

✅ Propiedades garantizadas

| Propiedad                               | ¿Cumple? |
|----------------------------------------|----------|
| Exclusión mutua en el buffer por slot  | ✅       |
| Orden de consumo por slot              | ✅       |
| Reutilización del slot solo tras n lecturas | ✅ |
| Independencia de tiempo entre consumidores | ✅ |
| Fairness (todos acceden eventualmente) | ✅       |


</details>

---

## 8) Implemente una butterfly barrier para 8 procesos

**Implemente una butterfly barrier para 8 procesos usando variables compartidas.**

<details><summary>Respuesta</summary>

Una **butterfly barrier** tiene **log2(n)** etapas.  
Cada Worker sincroniza con un Worker distinto en cada etapa.  
En particular, en la etapa `s` un Worker sincroniza con un Worker a distancia `2^(s-1)`.

Se usan distintas **variables flag** para cada barrera de dos procesos.

Cuando cada Worker pasó a través de `log2(n)` etapas, **todos los Workers deben haber arribado a la barrera** y por lo tanto **todos pueden seguir**.  
Esto es porque cada Worker ha sincronizado directa o indirectamente con cada uno de los otros.

**Diagrama (sincronizaciones por etapa)**

```text
Workers     1   2   3   4   5   6   7   8

Etapa 1     └───┘   └───┘   └───┘   └───┘

Etapa 2     └─────────┘   └─────────┘

Etapa 3     └───────────────────────┘
```

Codigo

```cpp
int N = 8;
int E = log(N);
int arribo[1:N] = ([N] 0);

process Worker[i = 1 to N] {
    int j;
    int resto;
    int distancia;

    while (true) {
        // Sección de código anterior a la barrera.

        // --- Inicio de la barrera butterfly ---
        for (etapa = 1; etapa <= E; etapa++) {
            distancia = 2 ^ (etapa - 1);           // distancia = 2^(etapa-1)
            resto = i mod 2 ^ etapa;

            if (resto == 0 || resto > distancia)   // define si sincroniza con i+dist o i-dist
                distancia = -distancia;

            j = i + distancia;

            while (arribo[i] == 1) skip;           // espera a que su flag esté en 0
            arribo[i] = 1;                         // indica que llegó

            while (arribo[j] == 0) skip;           // espera a su par
            arribo[j] = 0;                         // limpia la flag del otro
        }
        // --- Fin de la barrera butterfly ---

        // Sección de código posterior a la barrera.
    }
}
```

> Este no me quedo del todo claro pero bueno


</details>

---

## 9) Suponga `n^2` procesos organizados en forma de grilla cuadrada

Suponga **n^2** procesos organizados en forma de grilla cuadrada. Cada proceso puede comunicarse solo con los vecinos **izquierdo**, **derecho**, de arriba y de abajo (los procesos de las esquinas tienen solo **2** vecinos, y los otros en los bordes de la grilla tienen **3 vecinos**). Cada proceso tiene inicialmente un valor local **v**.

a) Escriba un algoritmo **heartbeat** que calcule el **máximo** y el **mínimo** de los **n2** valores. Al terminar el programa, cada proceso debe conocer ambos valores. (Nota: no es necesario que el algoritmo esté optimizado).

<details><summary>Respuesta</summary>

```cpp
Chan valores[1:n; 1:n](int);

Process P[i = 1 to n, j = 1 to n] {
    Int v;
    Int Nuevo, minimo = v, maximo = v;
    Int cantVecinos;
    Vecinos[1..cantVecinos];

    For (k = 1 to cantGeneraciones) {
        For (p = 1 to cantVecinos) {
            Send valores[vecinos[p].fila, vecinos[p].columna](v);
        }

        For (p = 1 to cantVecinos) {
            Receive valores[i, j](nuevo);
            if (nuevo < minimo)
                minimo = nuevo;
            if (nuevo > maximo)
                maximo = nuevo;
        }
    }
}
```

🎯 Supongamos 3 procesos: A, B, C

```text
A --- B --- C
```

- A tiene valor 5  
- B tiene valor 2  
- C tiene valor 8  

Cada uno está conectado con sus vecinos inmediatos.

🧪 Generación 1: Intercambio de valores

- 1. A envía 5 a B  
- 2. B envía 2 a A y C  
- 3. C envía 8 a B  

```text
     [5]        [2]        [8]
      A  <-->   B   <-->   C
```

🔍 ¿Qué recibe cada uno?

| Proceso | Recibe de | Valores recibidos | Nuevo mínimo | Nuevo máximo |
|---------|-----------|-------------------|---------------|---------------|
| A       | B         | [2]               | 2             | 5             |
| B       | A, C      | [5, 8]            | 2             | 8             |
| C       | B         | [2]               | 2             | 8             |

✅ Resultado final (después de 1 ronda)

```text
A: mínimo = 2, máximo = 5  
B: mínimo = 2, máximo = 8  
C: mínimo = 2, máximo = 8
```

Si hacemos otra ronda, **A también recibirá el 8 (a través de B)**, y entonces todos tendrán:

```text
mínimo = 2, máximo = 8
```

📌 Esto mismo pasa en grillas grandes: con varias generaciones, **los valores extremos se difunden**.

</details>

**b) Analice la solución desde el punto de vista del número de mensajes.**

<details><summary>Respuesta</summary>

En cada ronda, los procesos envían mensajes a sus vecinos. Dependiendo de su posición en la grilla, cada proceso tiene distinta cantidad de vecinos:

🔹 Esquinas (4 procesos)

- Cada uno tiene 2 vecinos → envía 2 mensajes por ronda
- Total por todas las rondas:
  
  ```
  4 procesos * 2 mensajes * (n-1) rondas * 2 (envío y recepción)  
  = 4 * 2 * (n - 1) * 2  
  = (n - 1) * 16 mensajes
  ```

🔹 Bordes (sin esquinas) → hay 4 lados con (n - 2) procesos cada uno

- Cada uno tiene 3 vecinos → envía 3 mensajes por ronda
- Total:
  
  ```
  (n - 2) * 4 procesos * 3 mensajes * (n - 1) rondas * 2  
  = (n - 2) * 4 * 3 * (n - 1) * 2  
  = (n - 1)(n - 2) * 12 mensajes
  ```


🔹 Internos → (n - 2) × (n - 2) procesos

- Cada uno tiene 4 vecinos → envía 4 mensajes por ronda
- Total:

  ```
  (n - 2)^2 * 4 mensajes * (n - 1) rondas * 2  
  = (n - 2)^2 * (n - 1) * 8 mensajes
  ```

</details>

> Este punto se podria mejorar

**c) ¿Puede realizar alguna mejora para reducir el número de mensajes?**

<details><summary>Respuesta</summary>

No, no es posible reducir el número de mensajes, ya que **no existe una forma de saber con certeza cuándo un proceso ha recibido el valor mínimo o máximo global**.  
Por lo tanto, para garantizar que **todos los procesos lleguen a conocer los valores extremos**, es necesario ejecutar las `(n - 1) × 2` generaciones completas.

</details>

---

> Voy a rezar por que no tomen esta wea

## 10) Una imagen se encuentra representada por una matriz

Suponga que una imagen se encuentra representada por una matriz a **(n×n)**, y que el valor de cada pixel es un número **entero** que es mantenido por un proceso distinto (es decir, el valor del píxel **I**,**J** está en el proceso **P(I,J)**). Cada proceso puede comunicarse solo con sus vecinos izquierdo, derecho, arriba y abajo. (Los procesos de las esquinas tienen solo 2 vecinos, y los otros bordes de la grilla tienen 3 vecinos).

**a)** Escriba un algoritmo **Herbeat** que calcule el **máximo** y el **mínimo** valor de los píxeles de la imagen. Al terminar el programa, cada proceso debe conocer ambos valores.

<details><summary>Respuesta</summary>

```nginx
chan topologia[1:n](emisor : int; listo : bool; top : [1:n,1:n] bool; max : int; min : int);

process nodo[p = 1..n] {
    bool vecinos[1:n];              # inicialmente vecinos[q] true si q es vecino de p
    bool activo[1:n] = vecinos;     # vecinos aún activos
    bool top[1:n,1:n] = ([n*n]false);  # vecinos conocidos (matriz de adyacencia)
    bool nuevatop[1:n,1:n];
    int r = 0;
    bool listo = false;
    int emisor;
    bool qlisto;
    int miValor, max, min;
    
    top[p,1..n] = vecinos;          # llena la fila para los vecinos
    max := miValor; 
    min := miValor;                # miValor inicializado con el valor del píxel

    while (not listo) {            # envía conocimiento local de la topología a sus vecinos
        for (q = 1 to n st activo[q]) {
            send topologia[q](p, false, top, max, min);
        }

        for (q = 1 to n st activo[q]) {
            receive topologia[p](emisor, qlisto, nuevatop, nuevoMax, nuevoMin);
            top = top or nuevatop;                  # hace OR con su top juntando la información
            if (nuevoMax > max) max := nuevoMax;    # actualiza los máximos y mínimos
            if (nuevoMin < min) min := nuevoMin;
            if (qlisto) activo[emisor] = false;
        }

        if (todas las filas de top tienen 1 entry true) listo = true;
        r := r + 1;
    }

    # envía topología completa a todos sus vecinos aún activos
    for (q = 1 to n st activo[q]) {
        send topologia[q](p, listo, top, max, min);
    }

    # recibe un mensaje de cada uno para limpiar el canal
    for (q = 1 to n st activo[q]) {
        receive topologia[p](emisor, d, nuevatop, nuevoMax, nuevoMin);
    }
}
```
</details>

**b) Analice la solución de desde el punto de vista del número de mensajes.**

<details><summary>Respuesta</summary>
Si M es el numero maximo de vecinos que puede tener un nodo, y D es el diametro de la
red, el número de mensajes maximo que pueden intercambiar es de 2n * m * (D+1). Esto
es porque cada nodo ejecuta a lo sumo D-1 rondas, y en cada una de ellas manda 2
mensajes a sus m vecinos
</details>


---

# Preguntas Teoricas Comunes

<div>
<img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExYmJtajN1emt3cGNnM205MWwyaGhqNXFvZHl0YnlmdTVtMzkzbGl0dyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/fYAX0DwcSYi0IggZMG/giphy.gif" width="500px">
</div>

---

## Pregunta 1 Ventajas y Desventajas


**3- Defina los paradigmas de interacción entre procesos distribuidos token passing, servidores replicados y prueba-eco. Marque ventajas y desventajas en cada uno de ellos cuando se utiliza comunicación por mensajes sincrónicos o asincrónicos.**

<details><summary><strong>Token Passing</strong></summary>

Es un esquema donde un mensaje especial (token) circula entre los procesos. Solo el que tiene el token puede ejecutar una acción crítica, como entrar a la sección crítica o tomar decisiones.

**Ejemplo:** exclusión mutua distribuida, detección de terminación.

**Ventajas:** simple de implementar, no necesita reloj ni identificadores globales, funciona bien en topologías como anillo.

**Desventajas:** si se pierde el token el sistema se bloquea; no hay paralelismo (solo trabaja quien tiene el token); puede haber demoras innecesarias.

**Mejor comunicación:** asincrónica, porque permite circulación sin bloqueo. Se adapta bien a arquitecturas de memoria distribuida (AMP).
</details>

<details><summary><strong>Servidores Replicados</strong></summary>

Varios procesos replican un recurso compartido (archivo, base de datos) para brindar alta disponibilidad y tolerancia a fallos. A los clientes les parece que hay un único servidor.

**Ejemplo:** mozos en el problema de los filósofos, sistemas de archivos distribuidos.

**Ventajas:** mayor disponibilidad, tolerancia a fallos, mejora el rendimiento si se balancean bien los pedidos.

**Desventajas:** mantener la consistencia entre réplicas es complejo; puede haber conflictos si dos servidores procesan escrituras en paralelo.

**Mejor comunicación:** asincrónica (evita bloquear al cliente), ideal en AMP. En SMP es más difícil porque hay que mantener varios canales y controlarlos.
</details>

<details><summary><strong>Prueba-Eco</strong></summary>

Un nodo envía mensajes “probe” a sus vecinos; cuando todos responden con “eco”, el emisor sabe que se llegó a todos. Sirve para explorar redes desconocidas o detectar nodos activos.

**Ejemplo:** descubrimiento de topología en redes móviles o dinámicas.

**Ventajas:** útil sin conocer la red; robusto frente a cambios; permite diseminar o recolectar información.

**Desventajas:** puede generar muchos mensajes; necesita control para evitar ciclos o duplicación.

**Mejor comunicación:** asincrónica, ideal en AMP por su descentralización y tolerancia a variaciones en la red.
</details>
