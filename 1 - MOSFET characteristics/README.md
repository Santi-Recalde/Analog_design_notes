### Regiones de operación de un MOS

Existen 2 principales regiones de operación de un MOS, una dividida en otras 2 subregiones. Estas son:

- Inversión débil o Subumbral (apagado)

    Esta región presenta una alta ganancia, aunque a costa de una baja $I_D$ o una alta W. Estos valores implican lentitud en la operación del dispositivo. Presenta una relación exponencial entre $V_{GS}$ e $I_D$. La misma se reduce a: (forma simplificada, supone $V_{DS}>100mV$)<br>
    <br>
    $I_D=I_0 e^{\frac{V_{GS}}{\zeta V_T}}$ <br>
    <br>
    Y en línea con esto, la ganancia $g_m$ se reduce a: <br>
    <br>
    $g_m = \frac{I_D}{\zeta V_T}$ <br>
    <br>
- Inversión fuerte (encendido)

    Se considera que esta etapa comienza cuando $V_{GS}$ supera el valor de $V_{TH}$, es decir el valor de umbral. Su diferencia se llama tensión de "overdrive" ($V_{OV}$), y es la variable de la que dependen las ecuaciones. <br>
    Esta región se divide en dos, definidas por el valor de $V_{DS}$ respecto a $V_{OV}$.

    - Triodo
        Cuando $V_{DS}$ < $V_{OV}$, se dice que el MOS opera en la región de triodo. En este punto, la corriente $I_D$ depende de $V_{DS}$ y de $V_{OV}$, siendo la primera una dependencia cuadrática negativa, y la segunda una dependencia lineal positiva. De esta manera resulta: <br>
        <br>
        $I_D = \frac{1}{2}{\mu}_n C_{ox} \frac{W}{L}[(V_{GS}-V_{TH})V_{DS}-V_{DS}^2]$ <br>
        <br>
        En esta región, la ganancia $g_m$ depende linealmente de $V_{DS}$ (cuidando que no se supere el umbral).

        - Triodo profundo
            Este modo particular de operación es el más utilizado en esta región. Consiste en aplicar $V_{DS}$ muy pequeñas. Esto reduce el término cuadrático a prácticamente 0, dejando solamente una dependencia lineal entre $V_{DS}$ e $I_D$. Esta dependencia se define por una resistencia $R_{on}=\frac{1}{{\mu}_n C_{ox} \frac{W}{L} (V_{GS}-V_{TH})}$. De esta manera se ve que se pueden implementar resistores mediante el uso de MOS.

    - Saturación
        Cuando $V_{DS}$>$V_{OV}$, se dice que el MOS opera en la región de saturación. Esta es la región más utilizada. En la misma, el MOS mantiene una corriente prácticamente constante frente a aumentos de $V_{DS}$. La fórmula que determina esto es la siguiente: <br>
        <br>
        $I_D=\frac{1}{2}{\mu}_n C_{ox} \frac{W}{L}(V_{GS}-V_{TH})^2$ <br>
        <br>
        Se puede notar que este es el máximo de la función cuadrática mostrada en la región de triodo. <br>
        Se debe contemplar que frente a mayores ${V_{DS}}_{sat}$, hay menos rango rango de tensión para señales amplificadas. <br>
        En este punto, el MOS opera como una fuente de corriente, la cual se puede aprovechar entre el drenador y su punto de referencia de tensión asociado en el circuito (depende de si es un NMOS o un PMOS). La resistencia asociada a esta fuente de tensión se define como $r_o$, y su existencia se debe a las variación de la longitud efectiva del canal de portadores en el MOS. Esta reducción de la longitud efectiva se modela como un termino lineal dependiente de $V_{DS}$ que se multiplica al valor de corriente definido por $V_{GS}$: <br>
        <br>
        $I_D=\frac{1}{2}{\mu}_n C_{ox} \frac{W}{L}(V_{GS}-V_{TH})^2 (1+\lambda V_{DS})$ <br>
        <br>
        Así surge la resistencia de salida del sistema: <br>
        <br>
        $r_o \approx \frac{1}{\lambda I_D}$, para $\lambda V_{DS}<<1$ <br>
        <br>
        Finalmente, la ganancia $g_m$ en esta región está dada por: <br>
        <br>
        $g_m={\mu}_n C_{ox} \frac{W}{L}(V_{GS}-V_{TH})(1+\lambda V_{DS})$ <br>
    <br>
> Superando cierta tensión de $V_{DS}$ se ingresa en una zona de ruptura, donde se destruye el MOS. Algo similar ocurre al superar cierta tensión de $V_{GS}$, donde se destruye el óxido que hace de aislante entre gate y sustrato.

El valor de tensión que diferencia a las regiones de inversión débil o fuerte, se define de una forma relativamente arbitraria, en base a garantizar continuidad entre las funciones de ganancia y corriente entre ambos modelos. <br>
Finalmente, haciendo una tabla comparativa resulta que las principales diferencias son:
| **Parámetro**  | **Inversión débil**                                   | **Triodo profundo**             | **Triodo**                                 | **Saturación**                                                            |
| -------------- | ----------------------------------------------------- | ------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------- |
| $g_m$          | alto: $g_m = \frac{I_D}{\zeta V_T}$    | bajo                            | crece con $V_{DS}$: $ g_m = {\mu}_n C_{ox} \frac{W}{L}V_{DS}$                         | depende de $V_{GS} $: $g_m = {\mu}_n C_{ox} \frac{W}{L}(V_{GS}-V_{TH})$                                               |
| $I_D$          | bajo, dependencia exponencial de $V_{GS}$                         | bajo                            | dependencia lineal de $V_{OV}$, y cuadrática de $V_{DS}$ | dependencia cuadrática de $V_{OV}$                                                    |
| **Ventaja**    | alta eficiencia de $g_m/I_D$, ideal para bajo consumo | actúa como resistor controlado  | útil como control variable de ganancia mediante $V_{DS}$     | fuente de corriente, buena linealidad y alta $r_o$                        |
| **Desventaja** | muy baja velocidad (por bajo $I_D$ y gran W)                   | tensión limitada, baja ganancia | región de transición, poco predecible      | para altas ganancias se reduce el rango de tensión  |
