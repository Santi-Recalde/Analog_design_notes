### Tipos de amplificadores de una etapa

Para simplificar todas las explicaciones partimos de la base de que para determinar la ganancia de un cuadripolo con comportamiento lineal, lo que se puede hacer es apicar el teorema de Norton: medir en los terminales de salida la corriente que circula cuando se cortocircuitan los mismos, y luego medir la resistencia de Thevenin en ese punto. El producto de ambas es el nivel de tensión que se tiene a la salida (tensión de Thevenin) (el análisis se hace con la corriente ya que la relación entre la tensión de entrada y de salida del sistema está dada por la corriente como intermediario, mediante la ganancia $g_m$)

1. **Surtidor común**

    Presenta una alta impedancia de entrada a bajas frecuencias, ya que la señal se introduce por el compuerta del MOS.
    La salida se obtiene desde el drenador del MOS.
    Su principio de funcionamiento se basa en forzar una corriente (controlada por la señal) por una carga y medir la caida de tensión respecto a $V_{DD}$ que se produce en la carga: esa es la señal de salida. Otra forma más acertada de verlo es que uno modifica la curva de corriente sobre la que está polarizado el transistor de entrada, lo que fuerza a que el propio transistor y el resto del sistema reaccione mediante cambios de tensión que mantengan válida la Ley de Voltaje de Kirchhoff (LVK). 

    > Esta configuración es inversora: aumentos en la entrada se mapean como disminuciones a la salida

    - **Resistor como carga**

        La ganancia está dada por: <br>
        <br>
        $A_v=-g_m \frac{r_o R_D}{r_o+R_D}$<br>
        <br>
        - Si el transistor ingresa a la región de triodo profundo, el sistema opera como un divisor resistivo
        - Se puede utilizar al sustrato como entrada, con $g_{mb}$ como la transconductancia
        - La impedancia a la salida esta dada por el paralelo de $r_o$ y $R_D$
        
        > La modulación del largo de canal es el único efecto considerable que afecta a esta configuración. No aparecen efectos con el sustrato.

    - **Configuración diodo-conectado como carga** (consideramos el transistor de entrada como M1 y al de carga como M2)

        Esta configuración consiste en un MOS con los terminales de drenador y compuerta conectados entre sí. Debido a esto, este se encuentra siempre en saturación, y se comporta como una resistencia (aunque con un nivel mínimo de tensión en sus terminales para operar sin caer en la región de subumbral). Este puede ser un NMOS o un PMOS, ambos se comportan de la misma manera, sin embargo, si el surtidor de cualquiera de estos se encuentra conectado a la salida en vez de a la misma tensión que el sustrato, aparecera el body effect.<br>
        <br>
        > La configuración de diodo-conectado es un operador de raiz cuadrada: la raiz cuadrada de la corriente que se fuerce a través de él será la que aparezca en sus terminales ($V_{GS2}$). Por este motivo, dado que la relación entre la tensión de entrada y la tensión de salida es lineal incluso para señales fuertes: $V_{GS1}$ modifica cuadráticamente a $I_D$, lo que luego se vuelve lineal al pasar por M2.

        La resistencia general, incluyendo el body effect e ignorando la modulación del largo del canal, que presenta el dispositivo esta dada por las transconductancias:<br>
        <br>
        $R_{diode\_ connected}=\frac{1}{g_m+g_{mb}}=\frac{1}{g_m}\frac{1}{1+\eta}$<br>
        <br>
        Así, la ganancia de la configuración termina definida como el producto de la ganancia $g_m$ del transistor que hace de entrada por esta resistencia. Sin embargo, al aplicarle el efecto de las modulaciones de canal de ambos transistores, se tiene que la resistencia de este transistor se ve en paralelo con las $r_o$ de los mismos. De esta manera la verdadera ganancia resulta ser, en el caso más general:<br>
        <br>
        $A_v=-g_{m1} \left( \frac{1}{g_{m2}+g_{mb2}}  \parallel  r_{o1}  \parallel  r_{o2} \right)$<br>
        <br>
        > El body effect puede evitarse utilizando tecnologías PMOS y NMOS de manera complementaria, aunque también a altas tensiones los efectos de variar la tensión del sustrato son menores.

        Por otro lado, si se despejan las relaciones, se puede obtener que la ganancia está definida realmente por las dimensiones que tengan ambos transistores. Por ejemplo, en el caso del NMOS + PMOS se tiene que la relación de ganancias se reduce a esta relación:<br>
        <br>
        $A_v=-\sqrt{\frac{\mu_n(W/L)_1}{\mu_p(W/L)_2}}$<br>
        <br>
        Por lo que se puede notar que para obtener grandes ganancias se deben incorporar grandes capacidades en la entrada o en la salida.<br>
        <br>
        Finalmente el siguiente problema que surje con esta configuración es la relación entre las tensiones de overdrive de ambos transistores, donde resulta que la misma es la ganancia: los aumentos de tensión de overdrive en la entrada se multiplican por la ganancia y se manifiestan en la tensión de overdrive de la carga. Dado que el rango dinámico de la tensión de salida tiene su cota inferior en $V_{GS1}-V_{TH1}$ y que la cota superior está dada por $V_{DD}-V_{TH2}$, un nivel de tensión de polarización excesivo en la entrada (en aras de aumentar la corriente, en consecuencia la transconductancia, y en última instancia la ganancia) puede limitar el rango dinámico debido a un mal posicionamiento del punto de tensión en el que se ubica la salida (no centrada en el rango dinámico). Para solucionar esto, se puede hacer uso de una fuente de corriente en paralelo a M2, que circule la corriente necesaria para polarizar a M1, y le deje a M2 la necesaria para obtener el nivel de tensión centrado (esto también reducirá el valor de $g_{m2}$).
        > Esta solución permite posicionar el nivel de tensión en continua, lo que parece reducir la ganancia. Esto es cierto, pero solo para la estática: la ganancia dinámica se mantiene constante, y puede ser utilizada para señales sin inconvenientes.

        - La impedancia de salida resulta $\frac{1}{g_{m2}+g_{mb2}}  \parallel  r_{o1}  \parallel  r_{o2}$
        - Superar el nivel de tensión superior introduce a M2 en la región de subumbral
        - Superar el nivel de tensión inferior introduce a M1 en la región de triodo
        
    - **Fuente de corriente como carga** (consideramos el transistor de entrada como M1 y al de carga como M2)

        En esta configuración se utiliza un transistor PMOS (si la entrada es NMOS y viceversa) operando en la región de saturación como fuente de corriente. De esta manera, la resistencia que hace de carga, es la propia dada por la modulación del largo del canal de M2, es decir, $r_{o2}$. Así la ganancia del circuito resulta ser:<br>
        <br>
        $Av= -g_{m1}(r_{o1} \parallel r_{o2})$<br>
        <br>
        Para mejorar la excursión de este circuito, se debe reducir la tensión de overdrive. Esto se logra mediante el aumento de $W_2$. Por otro lado, para aumentar $r_o2$ manteniendo la tensión de overdrive y la transconductancia constantes, se debe aumenar tanto $L_2$ como $W_2$. Como puede notarse, ambas soluciones implican aumentar la capacidad que se introduce a la salida.<br>
        <br>
        Los rangos de tensión que puede tomar $V_{out}$ están dados por aquellos valores que mantienen a ambos transistores operando en la región de saturación: el mínimo no puede ser menor a $V_{in}-V_{TH1}$, y el máximo no puede ser mayor a $V_{DD}-|V_{GS2}-V_{TH2}|$.

        - La impedancia de salida queda definida como $r_{o1} \parallel r_{o2}$
        - A mayor corriente menor ganancia, ya que reduce el valor de $r_o$ más rápido que lo que aumenta la transconductancia
        - A pesar de que aumentar L reduce la transconductancia, $r_o$ aumenta más rápido, lo que aumenta la ganancia

        > Se menciona que esta configuración debe utilizarse realimentada, ya que el punto de tensión a la salida en continua no está bien definido a lazo abierto.

    - **Carga activa complementaria (complementary CS stage)** (consideramos al transistor inferior NMOS como M1 y al transistor superior PMOS como  M2)

        La configuración de carga activa complementaria presenta la misma topología que la que utiliza una fuente de corriente como carga, con la diferencia de que tambien inyecta la señal a través de M2, es decir que ambas compuertas están conectados entre sí. Dado que un transistor es PMOS y el otro NMOS, los efectos que producen frente a la misma señal se refuerzan entre sí. Para comprender esto último, un aumento en la tensión de compuerta produce una reducción de la curva de corriente sobre la que opera M2, mientras que produce un aumento de la curva de corriente sobre la que opera el M1. Dado que ambas corrientes deben ser las mismas, M1 se ve obligado a aumentar su $V_{DS2}$ para compensar mediante la modulación de canal esta caida de corriente, mientras que por otro lado, M2 se ve obligado a reducir su $V_{DS1}$ para reducir la corriente que circula a través de él. Ambos efectos logran equilibrarse, y dado que la salida es el punto de tensión intermedio entre M2 y M1, ambos contribuyeron a la caida de tensión que se puede medir en $V_{out}$.
        
        > La  topología es la misma que la de un inversor CMOS

        Debido a lo mencionado anteriormente, la ganancia de esta topología aprovecha las transconductancias de ambos transistores. De esta manera:<br>
        <br>
        $Av=-(g_{m1}+g_{m2})(r_{o1} \parallel r_{o2})$<br>
        <br>
        El principal problema de esta configuración es que la corriente de polarización (y por ende todo el resto de parámetros asociados) depende fuertemente de PVT (proceso de fabricación, tensiones de operación, temperatura de trabajo). Un ejemplo de esto puede notarse en que $V_{GS1}+|V_{GS2}|=V_{DD}$, por lo tanto, variaciones en la alimentación modifican las $V_{GS}$, lo que termina modificando la corriente.<br>
        En línea con el ejemplo anterior, setiene que esta configuración es muy sensible a los ruidos de la fuente de alimentación: presenta la alrededor de la mitad de ganancia que la que se tiene desde la compuerta:<br>
        <br>
        $Av'=\left(g_{m2}+\frac{1}{r_{o2}}\right)(r_{o1} \parallel r_{o2})$
        <br>
        Los límites de la tensión de salida son los mismos que en el caso de la fuente de corriente como carga: el mínimo no puede ser menor a $V_{in}-V_{TH1}$, y el máximo no puede ser mayor a $V_{DD}-|V_{GS2}-V_{TH2}|$
        - La impedancia de salida es igual que en la fuente de corriente como carga: $(r_{o1} \parallel r_{o2})$
        - Se utiliza con realimentación en la mayoría de los casos para que funcione correctamente

    - **Transistor en region de triodo profundo como carga** (consideramos el transistor de entrada como M1 y al de carga como M2)

        Su principio de funcionamiento es simple: opera como una resistencia, de la cual es posible seleccionar su valor desde el compuerta de M2. Esto permite que se aplique el mismo análisis que el caso de resistencia de carga. De esta manera, la ganancia queda definida como:<br>
        <br>
        $A_v=-g_{m1} (r_{o1} \parallel R_{on2})$<br>
        <br>
        Donde la resistencia $R_{on2}$ es igual a:<br>
        <br>
        $R_{on2}=\frac{1}{\mu_p C_{ox} (W/L)_2 (V_{DD}-V_{G2}-|V_{TH2}|)}$<br>
        <br>
        Los límites de tensión admisibles a la salida para esta configuración están dados en su cota inferior por $V_{in}-V_{TH1}$ (para que M1 opere en saturación), y en su cota superior por $V_{DD}$ (para que M2 opere en triodo).
        - La impedancia de salida resulta del paralelo de ambas resistencias: $(r_{o1} \parallel R_{on2})$
        - Permite más rango de tensiones que la configuración diodo-conectado
        
        > Uno de los problemas que presenta esta configuración es que presenta dependencia al proceso de fabricación y a la temperatura.

    - **Transistor con degeneración de surtidor**

        Consiste en incorporar una resistencia en el surtidor, de manera que no conecte directamente con tierra. El objetivo de esto es hacer a la  ganancia menos dependiente de $g_m$, en particular de sus variaciones (las cuales introducian alinealidades).<br>
        El principio de funcionamiento de este principio es el mismo que el de una realimentación negativa, ya que frente a un aumento de la tensión en la compuerta se generaría un aumento en $V_{GS}$, lo cual produciría un aumento en la corriente. Este aumento en la corriente haría aumentar el nivel de tensión del surtidor (debido a la caida de tensión en la resistencia asociada), lo que reduciría el valor de $V_{GS}$, "amortiguando" el aumento de la corriente: realimentación negativa.
        Realizar esta realimentación modifica la ecuación de transconductancia, incorporando una nueva transconductancia: $G_{m}$. Esta nueva transconductancia, en su forma más básica está definida como:<br>
        <br>
        $G_m=\frac{g_m}{1+g_m R_S}$<br>
        <br>
        Con esta aproximación, se puede notar que si $R_S>>1/gm$, la transconductancia se reduce a la inversa de $R_S$, lo que linealiza la relación de $V_{in}$ con $I_D$ (en consecuencia $V_{out}$). <br>
        <br>
        En su forma general, considerando modulación del largo del canal y el body effect, la transconductacia $G_m$ resulta:<br>
        <br>
        $G_m=\frac{g_m r_o}{R_S+[1+(g_m+g_{mb})R_S]r_o}$<br>
        <br>
        En línea con esto, se puede probar que la impedancia de salida de la etapa sin carga está dada por el denominador de la transconductancia:<br>
        <br>
        $R_{out}=R_S+[1+(g_m+g_{mb})R_S]r_o =r_o+[1+(g_m+g_{mb})r_o]R_S$<br>
        <br>
        Con esto en mente, se puede proceder al cálculo de la ganancia del sistema frente al uso de una impedancia $R_D$. Para simplificar el análisis hacemos uso del producto de la ganancia por la resistencia de Thevenin. De esta manera y habiendo simplificado:<br>
        <br>
        $A_v=-G_m (R_D  \parallel  R_{out})=\frac{-g_m r_o R_D}{R_D+R_S+r_o+(g_m+g_{mb})R_S r_o}$<br>
        <br>
        > Una conclusión que se puede obtener del caso más general es que la ganancia del sistema puede definirse como el cociente entre la impedancia que se mide hacia el drenador (con el surtidor a tierra) sobre la impedancia que se mide hacia el surtidor (con el drenador a tierra) (algo útil en circuitos más complejos)
        
        Los rangos de tensión a los que puede acceder la salida se ven disminuidos por esta resistencia en el surtidor, ya que cuando la tensión busca bajar a la salida frente al aumento de la corriente, el punto de tensión en el surtidor aumenta debido a la resistencia. Por este motivo, el límite inferior de la tensión de salida resulta ser $V_{in}-V_{TH}$, mientras que el límite superior es $V_{DD}$ (si la carga es resistiva).

        Enumerando sus principales características se tiene que:
        - Suaviza alinealidades
        - Reduce la ganancia del sistema
        - Aumenta el ruido

        > Si se utiliza una fuente de corriente como carga (ideal), los efectos de la resistencia de source desaparecen, ya que al ser constante la corriente, no hay variaciones de tensión en el surtidor, lo que bloquea el efecto de realimentación, y resultando solamente en una reducción del rango dinámico de tensión que puede alcanzar la salida.


2. **Seguidor de surtidor**

    Presenta una alta impedancia de entrada a bajas frecuencias, ya que la señal se introduce por el compuerta del MOS.
    Esta configuración basa su principio de funcionamiento en obtener la señal de salida desde el surtidor del transistor: una resistencia de surtidor convierte en tensión las variaciones de corriente, y esta tensión en la señal a obtener. Desde la perspectiva de un sistema realimentado analizado en el caso de degeneración de surtidor, sería como obtener la señal realimentada, y dado que la realimentación es unitaria, se puede esperar que la ganancia tienda a la unidad.<br>
    Su utilidad radica en operar como un buffer tensión, aprovechando la alta ganancia de otras etapas sin comprometer sus propiedades. Un ejemplo de esto surge de analizar las configuraciones de surtidor común, donde la ganancia está determinada por la resistencia de la carga: si se varía la carga se varía la ganancia.<br>
    Esta operación como buffer le confiere ciertas capacidades para operar como adaptador de impedancias
    
    > Dado que la ganancia tiende a la unidad, es fácil deducir que esta configuración es no inversora.
    
    - **Polarización resistiva**

        Consiste en que la conexión de surtidor a tierra se haga mediante un resistor. Ignorando la modulación de ancho de canal, pero no el body effect, la ganancia resulta ser:<br>
        <br>
        $A_v=\frac{g_m R_S}{1+(g_b+g_{mb})R_S}≈\frac{1}{1+\eta}$<br>
        <br>
        Se puede ver como, a pesar de aumentar la ganancia o la resistencia de surtidor, debido al body effect es prácticamente imposible lograr una ganancia unitaria. Uno podría intentar aumentar el valor de la tensión surtidor-sustrato para reducir el valor de $\eta$, sin embargo debido a la tensiones disponibles este valor se mantiene mayor a 0,2.<br>
        Otra cuestión a considerar es que presenta cierta alinealidad en lo que respecta a la relación de de la salida con la entrada, a pesar de intentar ser un buffer. Esto ocurre ya que, si se analiza desde la perspectiva del control, el sistema es de tipo 0, por lo que existe siempre un error entre la entrada y la salida (incluso aunque la ganancia resultara efectivamente unitaria).<br>
        <br>
        La tensión de salida puede variar entre 0 y $V_{DD}+V_{TH}-V_{GS}$ (el valor de $V_{GS}$ depende de la corriente que circule), la verdadera limitación es que $V_{in}$ no debe superar $V_{DD}+V_{TH}$.
        - La resistencia de salida es $R_S  \parallel  \frac{1}{g_m}  \parallel  \frac{1}{g_{mb}}$, (no considera la modulación del largo del canal)

    - **Polarización con fuente de corriente** (se considera a M1 como el MOS de entrada y a M2 como la fuente de corriente)
        
        Esta configuración se sustituye la resistencia de surtidor por un MOS operando como fuente de corriente, implicando una mejora frente la configuración anterior. En esta se corrigen las alinealidades impuestas por tratarse de un sistema de tipo 0: dado que la corriente se vuelve constante (solo cambia el punto de tensión en el surtidor, es decir en la salida), la diferencia de tensión $V_{GS}$ debe mantenerse constante, por lo tanto, un aumento de X voltios en compuerta implica un aumento de X voltios también en surtidor. Este comportamiento mencionado es el ideal, ya que supone una ganancia igual a 1, algo que no se cumple debido al body effect y a la modulación del largo de canal.<br>
        > A pesar de que se resuelven ciertos problemas de alinealidad, aun se conservan justamente los relacionados al body effect (variación de $V_{TH1}$) y a la modulación del largo del canal (variación de $r_{o1}$).

        La incorporación de este MOS supone una reducción del rango dinámico de las tensiones en la salida, ya que la tensión no puede reducirse a un nivel inferior a $V_{GS2}-V_{TH2}$. Este nivel de tensión depende de la corriente de polarización que se desea que circule por la etapa. Para reducir la tensión de overdrive de M2 frente a una misma corriente podría aumentarse $W_2$, aunque esto implicaría un aumento de la capacidad asociada a la salida de esta etapa amplificadora. Por otra parte en lo que respecta a la tensión máxima esta se mantiene igual que en el caso anterior.<br>
        <br>
        En este caso más general, considerando la modulación del largo del canal y una carga $R_L$, la impedancia de salida resulta ser:<br>
        <br>
        $R_{out}=\frac{1}{g_m1}  \parallel  \frac{1}{g_{mb1}}  \parallel  r_{o1}  \parallel  r_{o2}  \parallel  R_L$<br>
        <br>
        Mediante el método de cálculo de la ganancia, esta resulta ser:<br>
        <br>
        $A_v=G_{m} R_{out} = g_{m1} \left(\frac{1}{g_{m1}+g_{mb1}+\frac{1}{r_{o1}}+\frac{1}{r_{o2}}+\frac{1}{R_L}}\right)=\frac{g_{m1}}{g_{m1}+g_{mb1}+\frac{1}{r_{o1}}+\frac{1}{r_{o2}}+\frac{1}{R_L}}$<br>
        <br>
        > El cálculo también puede hacerse desde la perspectiva de una red resistiva.
        
        - Es sensible al ruido
        - Presenta cierta utilidad en ajustar niveles de tensión

        > Los problemas de body effect pueden resolverse conectando el sustrato al surtidor, pero solo en los PFET, aunque hacer esto implica una mayor impedancia de salida a diferencia de los NFET.

        > **Debido a no ser tan eficientes, se los usa solo en casos donde sean absolutamente necesarios.**

3. **Compuerta común**

    Esta configuración, a diferencia de las otras dos, no inyecta la señal a través de la compuerta, sino que lo hace a través del surtidor. Esto tiene como consecuencia la existencia de una impedancia de entrada de valor finito. Por otro lado, la señal de salida se extrae del drenador.<br>
    Su principio de funcionamiento radica en modificar la tensión en el surtidor para afectar de esta manera a la tensión $V_{GS}$. La modificación de esta tensión implica una modificación de la corriente que circula a través de la carga asociada al drenador (similar al caso del surtidor común). Finalmente esta corriente origina una caida de tensión que es la que hace variar la señal de salida. Debido a que la señal se inyecta en un punto a través del cual también circula la corriente que origina la salida, para mantener a la fuente de señal fuera del camino de potencia, esta puede acoplarse en paralelo a la fuente de corriente que se ultilice para polarizarlo mediante una aislación capacitiva, o sino a través de otra etapa amplificadora, a través de un drenador (el cual puede hacer elemento de polarización también). A pesar de este detalle, se puede analizar su comportamiento mediante una fuente de tesión conectada directamente en el surtidor (se puede incorporar una resistencia en serie para evaluar su comportamiento en ese caso).<br>
    Su principal atributo es que permite adaptar impedancias para evitar reflexiones, a la vez que potencia la ganancia de la etapa mediante el body effect.<br>
    <br>
    Para que esta etapa funcione, la tensión en surtidor debe ser menor a $V_G-V_{TH}$ (ya que si no el transistor entraría en la región de subumbral), y debe ser mayor a la tensión mínima de operación que requiere el elemento de polarización o entrada de señal para operar correctamente ($V_{in1}$).<br>

    > Dado que la salida a través del drenador depende inversamente de la tensión $V_{GS}$ (tal y como se vió en el análisis de surtidor común), y que el valor de $V_{GS}$ depende inversamente de la tensión en el surtidor, esta configuración es no inversora.

    > Como se verá a continuación, aquello que limita la excursión de la entrada y la salida es la tensión de compuerta, por lo que debe seleccionarse a consciencia. Se menciona también en relación a esto que, dado que entrada y salida comparten red, el rango de tensiones alcanzables a la salida se encuentra limitada por el rango de tensiones que debe tener la entrada.

    - **Resistor como carga**

        Esta configuración utiliza las caidas de tensión a través de un resistor para modificar la tensión en el drenador mediante las variaciones de corriente. Considerando que la señal a la entrada (en surtidor) presenta una resistencia en serie $R_S$, la ganancia del sistema resulta definida como:<br>
        <br>
        $A_v= \frac{(g_m+g_{mb})r_o + 1}{r_o + (g_m +g_{mb})r_o R_S + R_S + R_D}R_D$<br>
        <br>
        Debido a las características del circuito, este puede operar enteramente en la región de saturación, sin entrar nunca a la de triodo, como también puede operar enteramente en la región de triodo, sin entrar nunca a la de saturación. En el caso de saturación, esto se logra mediante la elección de una impedancia en la carga que, a la corriente máxima ($V_S = 0$), posicione al drenador en un nivel de tensión superior a la tensión de overdrive (que va a disminuir a medida que aumente $V_{in}$, aumentando aún más el valor de la tensión de salida). El caso de triodo no es deseable, así que se ignora su análisis.<br>
        <br>
        En línea con esto, se puede ver que operando en la región de saturación, el rango de tensiones de salida oscila entre un máximo de $V_{DD}$ y un mínimo de $V_{G}-V_{TH}$ (para que el dispositivo se mantenga en la región de saturación).<br>

        - La impedancia de entrada de esta configuración es: $R_{in}= \frac{R_D+r_o}{1+(g_m+g_{mb})r_o}$
        - La impedancia de salida de esta configuración es: $R_{out}= [R_S + (g_m+g_{mb})r_o R_S + r_o] \parallel R_D$

    - **Fuente de corriente como carga** (se considera una fuente de corriente ideal)

        Se modela de similar forma que el caso con carga resistiva, pero considerando que $R_D$ tiende a infinito. En consecuencia, la ganancia se reduce a:<br>
        <br>
        $A_v= (g_m+g_{mb})r_o + 1$<br>
        <br>
        Los rangos de tensión a la salida, como es de esperarse, se ven reducidos debido a la tensión mínima $V_{DSmin}$ que debe conservar el transistor que hace de fuente de corriente para evitar caer en la zona de triodo. De esta manera, los límites de tensión resultan estar en un máximo de $V_{DD}-V_{DSmin}$ y un mínimo de $V_{G}-V_{TH}$.
        Por otro lado, también implica los siguientes comportamientos:
        
        - La impedancia de entrada se vuelve infinita
        - La impedancia de salida de esta configuración resulta ser: $R_{S} + (g_m+g_{mb})r_o R_S + r_o$
        - La corriente en la etapa no varía (por eso la impedancia de entrada es infinita)

    > Respecto a esta configuración, se menciona que los límite de $V_G$ están dados en su cota inferior por $V_{in1}+V_{TH}$, y en su cota máxima por la tensión mínima que se busque en el rango de operacion del MOS

    > También se menciona que la señal de entrada puede ser una señal de corriente, a diferencia de las otras etapas donde la entrada debía ser siempre una tensión
    
4. **Cascode** (se considera como M1 al MOS que opera como entrada y se considera como M2 al MOS que opera como cascode)

    Esta configuración consiste en la utilzación simultánea de dos etapas: una etapa CS y una etapa CG. A la etapa CS se la conoce como dispositivo de entrada, y a la etapa CG se la conoce como dispositivo cascode. Esta última puede tener un resistor como carga o una fuente de corriente como carga.<br>
    Su principio de funcionamiento se basa en la utilización de la etapa CS como una señal de corriente que se inyecta desde el surtidor de M2, forzando esa misma corriente a través del drenador de este mismo MOS. Por lo tanto, la ganancia se reduce a la propia de una etapa CS. Sin embargo, la principal ventaja de esta configuración es la alta impedancia de salida que presenta, algo que permite aumentar la ganancia intrínseca del conjunto, en condiciones de un $R_D$ infinita.

    > En caso de intentar inyectar señal por el MOS cascode, esto no producirá variaciones en la salida, ya que la corriente esta fijada por el MOS de entrada. En estas condiciones el conjunto se comporta de la misma manera que un seguidor de surtidor.

    > Como puede anticiparse, dado que se trata de una etapa inversora en cascada con una etapa no inversora, el conjunto funciona invirtiendo la salida.

    - **Telescópico**

        En este caso los MOS que constituyen esta etapa son un par de NMOS o un par de PMOS según sea el caso.<br>
        Dado que la salida se encuentra sobre dos MOS, esta no puede ser menor a las dos tensiones de overdrive necesarias para que el conjunto funcione: $V_{out} ≥ V_{GS1}-V_{TH1}+V_{GS2}-V_{TH2} $. Sin embargo, un límite más estático es que la salida no puede ser menor que $V_{G2}-V_{TH2}$, y el valor de tensión en la compuerta del MOS cascode debe cumplir que $V_{G2}>V_{TH2}-V_{D1}>V_{TH2}-V_{in}+V_{TH1}$.<br>
        A medida que se reduce $V_{out}$, los niveles de tensión del conjunto determinarán que MOS entrará primero en la región de triodo: si $V_{out}$ cae por debajo de $V_{G2}$ una cantidad superior a $V_{TH2}$ quien cae en la región de triodo es M2, sin embargo, si $V_{in}$ supera por $V_{TH1}$ a la tensión $V_{D1}$, es M1 quien ingresa en primer lugar a la región de triodo.<br>
        <br>
        Como se dijo anteriormente, la principal ventaja de esta configuración es su alta impedancia de salida. Para deducirla se hace uso de la ecuación planteada en la etapa CS, para el caso con degeneración de surtidor, considerando que la resistencia asociada a M1 es $r_{o1}$ y una impedancia de carga infinita (fuente de corriente ideal). De esta manera resulta: (el resultado también coincide con el planteado en la etapa CG)<br>
        <br>
        $R_{out}=[1+(g_{m2}+g_{mb2})r_{o2}]r_{o1}+r_{o2}≈(g_{m2}+g_{mb2})r_{o2}r_{o1}$<br>
        <br>
        Como puede notarse, la impedancia de salida de la configuración CS se ve potenciada por el MOS M2. Siguiendo con está lógica, agregar más etapas CG seguría aumentando la impedancia de salida, pero a costa de aumentar el límite inferior de la tensión de salida (sumando más tensiones de overdrive a la "pila").<br>
        <br>
        En lo que refiere a la transconductancia del sistema, esta aunque en una primera aproximación parezca ser $g_{m1}$, se puede notar que será ligeramente menor, ya que una pequeña parte de la misma se filtra a través de $r_{o1}$, lo que reduce la que pasa por la etapa CG. Con esto en mente, haciendo un análisis de divisores de corriente, resulta que la transconductancia es:<br>
        <br>
        $G_m= \frac{g_{m1}[r_{o1}+r_{o1}r_{o2}(g_{m2}+g_{mb2})]}{r_{o1}+r_{o1}r_{o2}(g_{m2}+g_{mb2})+r_{o2}}$<br>
        <br>
        Con esto en mente, y haciendo uso del principio enunciado acerca de la ganancia, la ganancia intrínseca de esta etapa resulta ser:<br>
        <br>
        $A_v= -g_{m1} [r_{o1}+(g_{m2}+g_{mb2})r_{o2}r_{o1}] ≈ -g_{m1}(g_{m2}+g_{mb2})r_{o2}r_{o1}$<br>
        <br>
        Por otro lado, debido a su alta impedancia de salida, son **excelentes fuentes de corriente**. Esto puede aprovecharse justamente para crear mediante PMOS la fuente de corriente ideal que debe alimentar a la etapa amplificadora. Las consecuencias de hacer esto es que ahora la reducción de rango dinámico es de 4 tensiones de overdrive. Mientras tanto, analizando la impedancia de salida, esta queda definida como el paralelo de ambos conjuntos: (M3 como cascode y M4 como "entrada")<br>
        <br>
        $R_{out}'=[1+(g_{m2}+g_{mb2})r_{o2}]r_{o1}+r_{o2}  \parallel  [1+(g_{m3}+g_{mb3})r_{o3}]r_{o4}+r_{o3} $<br>
        <br>
        Y entonces la ganancia se reduce a:<br>
        <br>
        $A_v' ≈ -g_{m1}[(g_{m2}+g_{mb2})r_{o2}r_{o1} \parallel (g_{m3}+g_{mb3})r_{o3}r_{o4}]$ <br>
        <br>

        > Frente a un rango de tensiones definido, es la configuración que maximiza la impedancia de salida (conservando la ganancia del sistema).

        Existe na configuración llamada **Poor Man's Cascode**, la cual vincula las compuertas de ambos MOS a la misma señal. Esto, si ambos son iguales, lleva a que el MOS CS opere en la región de triodo. Sin embargo, si se varían las $V_TH$ para que la de CS sea menor que la de CG, ambos operan como un cascode (cuidando el rango de tensiones).<br>
        <br>
        Otra característica a considerar es que dada la alta impedancia de salida, esta **blinda** al dispositivo de entrada en el surtidor del MOS CG frente a variaciones de tensión a la salida (en el drain del mismo MOS) (por ejemplo puede minimizar las variaciones de corriente entre fuentes de corriente debidas a diferencia de tensiones en sus terminales)(esta protección desaparece si el cascode entra en región de triodo).

        > Debido a que su funcionamiento se basa en dos fuente de corriente en serie, es necesario incorporar lazos de realimentación para que el sistema sea estable.

    - **Folded** (se considera a M3 como la fuente de corriente que alimenta a ambos MOS)

        Consiste en un cascode hecho con un NMOS como entrada y un PMOS como cascode (o viceversa) conectados a tierra (o a $V_{DD}$) a través de una fuente de corriente, balanceando la  corriente que circula entre ellos según la tensión de entrada. Este balanceo es el que logra variar la tensión a la salida: cuando toda la corriente pasa por M2, la tensión de salida es mínima, y cuando toda la corriente pasa por M1, la tensión de salida es máxima.

        > Dado que la corriente se divide entre ambos, la fuente de corriente debe manejar el doble corriente que se desea que pase por cada MOS. 

        Para determinar la resistencia de salida, nuevamente se aplica el criterio de CS con degeneración de surtidor, con la diferencia de que en este caso la resistencia asociada al surtidor de M2 es el paralelo de $r_{o1}$ y $r_{o3}$. De esta manera la resistencia de salida resulta:<br>
        <br>
        $R_{out} = [1+(g_{m2}+g_{mb2})r_{o2}](r_{o1} \parallel r_{o3})+r_{o2}$<br>
        <br>
        Se puede notar que la impedancia de salida es menor en este caso. Suponiendo que $r_{o1}=r_{o3}$, esta impedancia sería la mitad que su análogo telescópico.<br>
        <br>
        En consecuencia con esto, se puede rápidamente notar que la ganancia intrínseca de esta configuración también se ve reducida. Resultado ser: (considerando una carga de salida con impedancia infinita)<br>
        <br>
        $A_v ≈ -g_{m1}(g_{m2}+g_{mb2})r_{o2}(r_{o1} \parallel r_{o3})$<br>
        <br>
        > Para acercarse a esta condición, se puede hacer uso de una etapa cascode telescópica para hacer de carga en el drenador de M2.

        Los rangos de tensiones a la salida son similares al caso anterior.

#### Diferencias entre los modelos de señal fuerte y señal débil

En todas estas etapas de amplificadores se puede plantear un modelo de señal fuerte y un modelo de señal débil, los cuales presentan utilidades diferentes en relación a lo que se busque analizar del circuito.

##### **Señal fuerte**

El modelo de señal fuerte se refiere a las relaciones matemáticas que existen entre los parámetros de mi circuito, a la función en sí misma que vincula un parámetro con otro: cierta cantidad de un elemento X se corresponde exactamente con cierta cantidad de un elemento Y, por lo que cuando hablamos de estas relaciones, hablamos de relaciones **absolutas**.<br>
Un ejemplo de esto puede ser la relación cuadrática que existe entre la tensión de overdrive y la corriente que circula por el MOS, donde si la tensión de overdrive es $2 V$ entonces la corriente de drenador va a ser proporcional a $4 V^2$ ($2 V$ al cuadrado).<br>
Este modelo es de gran utilidad cuando se deben hacer los análisis de polarización del dispositivo, como también cuando se deben analizar los límites de tensión de operación del circuito, o las características que va a tener el mismo operando en distintos puntos. Permite también reconocer las alinealidades y tipo de relaciones que terminan existiendo entre las variables.

##### **Señal débil**

El modelo de señal débil se refiere a las relaciones matemáticas que existen entre las variaciones de los parametros de mi circuito: son las derivadas de mis funciones de señal fuerte, las cuales aplicando el principio de series de Taylor, buscan aproximarse al modelo de señal fuerte en un rango acotado, manifestando comportamientos cuasilineales que son de gran utilidad. Cuando hablamos de estas relaciones, hablamos de relaciones **relativas**, ya que se cumplen solamente alrededor de un punto de operación que funge como centro del entorno de validez de las relaciones que se manifiestan entre los parametros, los cuales ahora en vez de definirse como su totalidad, se definen como su valor respecto a la polarización. Estas aproximaciones suponen que las relaciones entre parametros son lineales, ya que los valúan en un punto y suponen que la variación es suficientemente pequeña como para que no cambien las características del circuito en ese intervalo. De esta manera se puede considerar que la transconductancia de mi circuito no cambia en un intervalo pequeño de variaciones de la tension de overdrive, por lo que los cambios en la tensión de overdrive se mapean linealmente con los cambios de la corriente de drenador.<br>
Un ejemplo de esto podría ser una situación donde mi circuito se encuentra polarizado en $2 V$ en tensión de overdrive, correspondiendo esto con $100 mA$ de corriente de drenador, lo que implica una transconductancia de $100 \frac{mA}{V}$. Este resultado surge de un analisis de señal fuerte, pero aplicando señal débil podemos decir que, por ejemplo, si la tensión de overdrive aumenta $20 mV$, la corriente de polarización va aumentar $2 mA$. Si aplicamos señal fuerte, este aumento implicaría un aumento de la corriente de $2.01 mA$. Como se puede notar, la diferencia es del 0.5%, algo despreciable.<br>
Este modelo es de gran utilidad cuando se deben hacer analisis del comportamiento del circuito frente a señales muy pequeñas, y se busquen minimizar las operaciones o las complicaciones de cálculos a las que se deberían incurrir para hacer análisis de señal fuerte.
