# Laboratorio-5_PDS
# Descripcion


Este proyecto abarca el código y el procedimiento necesario para realizar un análisis de la variabilidad de la frecuencia cardíaca (HRV) a partir de señales ECG, utilizando herramientas de procesamiento digital como la transformada wavelet. Empleando Python y bibliotecas especializadas como PyWavelets, se desarrollan cálculos tanto en el dominio del tiempo como en el dominio tiempo-frecuencia, lo cual permite identificar las fluctuaciones en los intervalos R-R y su relación con la actividad simpática y parasimpática del sistema nervioso autónomo. El análisis incluye el diseño e implementación de filtros digitales, la detección de picos R, y la obtención de espectrogramas, proporcionando así una comprensión más profunda de la dinámica temporal de la señal cardíaca. Gracias a estos métodos, se logra visualizar y explicar de manera crítica cómo varían las frecuencias a lo largo del tiempo, facilitando el estudio de la HRV como una herramienta diagnóstica y de investigación en el campo biomédico.


## Fundamento Teórico
### Sistema Nervioso Autónomo (SNA)
Es la parte funcional del sistema nervioso que se encarga de la regulación de las funciones viscerales involuntarias del organismo, mantiene la homeostasis y controla la presión arterial, la frecuencia cardiaca, entre otros. Se puede dividir funcionalmente en simpático y parasimpático

#### Simpático
Es controlado por los nervios simpáticos y tienen su origen en la medula espinal, se encarga de acelerar el ritmo cardiaco y llevar mas sangre a las zonas del cuerpo donde se necesita más oxígeno. De igual manera afecta al sistema inmunitario y la reparación del cuerpo. En resumen, el sistema nervioso simpático se encarga de transmitir señales de alerta al cuerpo.

#### Parasimpático
Este sistema se encarga de relajar el cuerpo tras periodos de estrés o peligro. Por otra parte, ayuda a ejecutar procesos vitales, como la digestión y los momentos de relajación. Permite controlar la frecuencia cardiaca, la sudoración, entre otros.

### Efecto en la frecuencia Cardiaca
La actividad simpática, normalmente aumenta la frecuencia cardiaca, la fuerza de las contracciones del musculo cardiaco y dilata las vías respiratorias para mejorar la respiración e igualmente permite al organismo liberar la energía almacenada. Cuando la rama simpática está más activa, la frecuencia cardíaca suele aumentar y late a un ritmo más regular reduciendo la variabilidad de la frecuencia.

Por otra parte, el sistema parasimpático reduce la frecuencia cardiaca y la fuerza de contracción del corazón (vasoconstricción) para relajar el sistema del cuerpo, la rama parasimpática es la parte más relajada que simplemente zumba cuando está relajado aumentando la variabilidad de la frecuencia en las altas frecuencias.

### HRV (Variabilidad Frecuencia Cardiaca)
Es la variación en el tiempo de los latidos consecutivos es decir de la frecuencia cardiaca (R-R en un ECG). El corazón se controla por medio del SNA,  la parte involuntaria del sistema nervioso, por lo tanto, cuando la rama parasimpática esta mas activa la HRV aumenta y cuando se activa la simpática la HRV disminuye.

Por lo cual la HRV es un indicador del equilibrio entre la actividad de las dos ramas del sistema nervioso autónomo, esto hace que sea una medida indirecta del estrés, una mayor HRV indica un menor estrés 

La fluctuación de la HRV se debe analizar en una serie de intervalos R-R registrados en un periodo de tiempo que debe ser aproximadamente de 5 minutos mínimo, se calcula como cambian estos valores de un latido al siguiente. Para analizar la frecuencia de las HRV se tiene en cuenta la banda de frecuencia yy el rango de cada una:

•	Potencia de alta frecuencia: rango de 0.15 a 0.40 Hz  (parasimpatico)

•	Potencia de baja frecuencia: rango de 0.04 a 0.15 Hz (mezcla de simpatico y parasimpatico)

•	Relacion LF/HF: Relacion entre baja y alta frecuencia, es decir el equilibrio autónomo entre simpatico-parasimpatico. Rango de 0.003 a 0.04

### Transformada Wavelet 
La transformada wavelet es una herramienta matemática que permite obtener diversas aplicaciones en el procesamiento de señales y especialmente en detección de anomalías en medicina. Estas transformadas permiten representaciones de funciones en las cuales se retiene tanto la escala como la información espacial.

Permite descomponer señal en componentes que tienen resolución en el tiempo y en la frecuencia, ideal para señales no estacionarias (que cambian en el tiempo), como las señales biológicas. A diferencia de la Transformada de Fourier, que solo da información de frecuencia global, la wavelet permite identificar cuándo ocurren los cambios en frecuencia.

Existe la transformada Wavelet discreta (DWT) que se usa principalmente para descomponer la señal en diferentes escalas y eliminar el ruido. La transformada Wavelet Continua (CWT) que permite ver una señal mas detallada y para señales fisiológicas para estudiar la variación de la frecuencia a lo largo del tiempo

Tipos de transformada Wavelet:

•	Daubechies:  Se caracteriza por tener gran compactación del soporte y de igual manera detectas cambios bruscos o discontinuidades en una señal. Es esencial para eliminar el ruido y lograr analizar los datos

•	Symlets: Reducen los artefactos al reconstruir una señal y logran mantener una buena localización en el tiempo y frecuencias, reconstruye de forma precisa las señales sin distorsión


•	Coiflets: Presentan una alta regularidad y momentos nulos como la función de escala, por otro lado, cuentan con una mejor localización en tiempo y frecuencia que Daubechies, son una buena opción para analizar señales suaves con cambios graduales y caracterizar la forma de ondas


•	Morlet: Es una onda senoidal modulada por una función gaussiana, cuenta con una excelente resolución en frecuencia, pero con menos tiempo, estudia normalmente las oscilaciones y eventos transitorios, pero no se usa para comprensión si no únicamente para análisis continuo 


•	Mexican Hat: Es de forma acampanada y es una segunda derivada de una función gaussiana, es una gran opción para detectar picos o eventos únicos en la señal, como eventos de corta duración.

•	Haar:  Es la wavelet mas simple ya que presenta una forma cuadrada y discontinua, presenta una gran localización temporal, pero con muy poca en frecuencia y se especializa en señales digitales con saltos abruptos. 


•	Meyer: Es una wavelet totalmente suave e infinitamente diferencial, no cuenta con un soporte compacto en el tiempo, pero si en la frecuencia, permite de igual manera una transición suave entre bandas de frecuencia.

•	Beylkin: Se usa en algoritmos de comprensión y solución matemática de ecuaciones integrales, tiene un alto numero de momentos nulos que permite que sea ideal para representar funciones suaves como de campo electromagnético

•	Battle-Lemarie: Se basa en funciones polinómicas por tramos y tienen una buena localización en frecuencia, les da continuidad y suavidad deseables, presenta un buen balance entre tiempo y frecuencia

![image](https://github.com/user-attachments/assets/a091bb30-9669-4541-a3ac-ddc854d2c41a)
*Tipos de Wavelets*

Las Wavelets mas usadas para señales fisiológicas son las primeras 5 mencionadas ya que cada una como se menciona anteriormente, cuenta con aspectos importantes como eliminación de ruido, controlar ya sean frecuencias altas o bajas y estas señales (EEG, ECG, EMG) necesitan un mayor análisis y detección de patrones. 

## Adquisición de la señal ECG
Para realizar la adquisición de la señal ECG (electrocardiograma) se utilizo una DAQ (Data Acquisition Device) como sistema de adquisición de datos, se realizo la connfiguración adecuada para capturar de forma continua la señal del corazón durante un periodo total de 6 minutos. La señal se divide en dos etapas: los primeros 3 minutos corresponden a una fase de relajación, donde la persona esta en reposo, tranquila y sentada o recostada, para obtener una línea base de la actividad cardíaca bajo influencia predominante del sistema nervioso parasimpático. Posteriormente, se inicia la fase de estrés o estimulación, también de 3 minutos, en la que se induce un aumento en la frecuencia cardíaca por medio de un juego que eleva el estres, con el objetivo de activar el sistema nervioso simpático. Durante toda la adquisición, la DAQ esta conectada a electrodos de superficie colocados en el cuerpo y se configura con una frecuencia de muestreo adecuada (en este caso 1000 Hz) para capturar con precisión las ondas del ECG, especialmente los intervalos R-R que luego se analizarán para calcular la variabilidad de la frecuencia cardíaca (HRV) y observar las diferencias fisiológicas entre ambos estados.

![image](https://github.com/user-attachments/assets/1e2e2887-9f9a-466a-a795-12f7cae78d15)

*Ubicación de los electrodos para ECG*

## Pre-Procesamiento de la señal
En el siguiente paso, se realiza el pre procesamiento de la señal por medio de un filtro IIR para observar la señal ECG de manera adecuada y posteriormente realizar el análisis respectivo de ella. Se realiza un Filtro Butterworth con los siguientes parámetros.
![image](https://github.com/user-attachments/assets/07d50577-7204-4c06-8179-10902cc4ecda)

*Parámetros para el diseño del filtro*

En el cual se establece un filtro que cuenta con una frecuencia de muestreo de 1000 Hz y dos frecuencias de corte entre 0.5 y 40 Hz que son las frecuencias ideales para obtener la mayoría de la energía útil del ECG. La frecuencia de corte baja de 0.5 Hz se encarga de eliminar la línea base es decir el ruido como movimientos o respiración durante la captura de la señal, y la frecuencia de corte alta de 40 Hz elimina el ruido de alta frecuencia preservando las ondas, P, QRS y T. 

Por otro lado, se escoge el filtro Butterworth debido a su respuesta suave y sin ondulaciones que permite preservar bien la forma de la señal. El orden del filtro se establece como 4 ya que mantiene la estabilidad de la señal y proporciona una pendiente adecuada, eliminando componentes fuera de 0.5-40 Hz y sin amplificar el ruido por resonancias.

![image](https://github.com/user-attachments/assets/05827070-a690-4606-a423-f151edf118b1)

*Normalización de la señal*

Esto se realiza ya que los filtros digitales como el realizado trabajan en el dominio discreto, por lo cual se usa la frecuencia de Nyquist que es la mitad de la frecuencia de muestreo, para así poder observar la señal normalizada y convertir las frecuencias en Hz a frecuencias digitales normalizadas. 

![image](https://github.com/user-attachments/assets/8ff9a91e-3468-42ad-9c4d-199bacde7653)

*Calculo de coeficientes*

Una vez normalizadas las frecuencias se calculan los coeficientes de la ecuación donde se colocan las bandas de paso y de rechazo, de igual manera devuelve los coeficientes del filtro donde b es la entrada y a la salida, los cuales definen el filtro en forma de sistema recursivo lineal (IIR).

![image](https://github.com/user-attachments/assets/b3eac311-bd5d-4fe9-882e-612eedf4cedb)

*Ecuación en diferencias del filtro IIR*

Esta sección del código aplica el filtro IIR directamente, usando la ecuación en diferencias que representa la versión discreta en la función de transferencia. Con la siguiente ecuación se realiza la sección del código:

![image](https://github.com/user-attachments/assets/300b4510-cf01-4f4a-9905-29782ce4719d)

*Ecuación general en diferencias* 

Esta ecuación permite aplicar el filtro como se menciono anteriormente, y ya una vez en el código se aplica manualmente desde cero con las condiciones iniciales en 0, permitiendo que recorra cada muestra de la señal de entrada y se calcula la señal filtrada sumando cada termino del numerador y restando las contribuciones de salidas pasadas según la ecuación. Esto permite que el filtro tenga memoria y actúa como IIR.

Ya una vez aplicado el codigo se observa la señal orginial y la señal filtrada, por lo que se puede observar que como la captura duro 6 minutos (360 segundos) no se observa adecuadamente el filtrado de la señal, pero al palicar el filtro a una pequeña parte de la señal se observa como el filtro cumple con eliminar el ruido y actua como filtro pasa banda permitiendo frecuencias de unicamente 0.5-40 Hz.

![image](https://github.com/user-attachments/assets/f17038a4-0b64-497f-af4b-aaf0d74faca0)
*Comparación de señal orginal y filtrada (360 segundos)*


Teniendo la señal ya filtrada, de acuerdo con lo explicado anteriormente, se procede con el proceso de detección de los picos R, los cuales corresponden a los máximos del complejo QRS en la señal ECG y representan los instantes de cada latido cardíaco. A partir de estos picos, es posible calcular los intervalos R-R, definidos como el tiempo entre latidos consecutivos. Esta información permite construir una nueva señal que refleja la variabilidad de la frecuencia cardíaca (HRV), la cual es esencial para el análisis en el dominio del tiempo y en el dominio tiempo-frecuencia, como parte del estudio de la actividad del sistema nervioso autónomo.
En primera medida, lo que se hace es entender de forma correcta para que funciona todo esto, los picos R son aquellos puntos más altos de cada complejo QRS en un ECG, estos lo que hacen es representar la despolarización de los ventrículos, en términos más sencillos el momento de contracción de los ventrículos del corazón, son picos detectables y que marcan los instantes de cada latido. 

![image](https://github.com/user-attachments/assets/f93d8397-8f2a-468d-bd9e-b75b14139b17)


*Detección de los picos R en Python.*

En el código la función find_peaks lo que hace es buscar los máximos locales en la señal ya previamente filtrada, por otro lado, height=0.5 evita que el ruido que aún persiste lo detecte como pico por ende soloo considera como pico auqellos de amplitud mayor a 0.5 y la distance=int(0.6* fs) impone que haya al menos 0.6 s entre picos ya que es una equivalencia a la frecuencia cardiaca máxima de 100lpm y finalmente tiempos_picos es el vector de tiempo que corresponde a los picos, esto es bastante importante ya que su identificación precisa es la base para un análisis HRV adecuado. 

![image](https://github.com/user-attachments/assets/9d6119a9-c422-4f4a-9b89-a76b269f3240)


*Picos R de la señal filtrada.*

Por otro lado, los intervalos R-R son el paso siguiente ya que es el tiempo entre un pico R y el siguiente y esto es una medida de la frecuencia cardiaca instantánea. Gracias a estos intervalos se puede ver como varia el tiempo entre latidos, esto indica que el sistema nervioso autónomo está actuando sobre el corazón. 

![image](https://github.com/user-attachments/assets/94347c20-cdc6-418d-a01c-33e6fbb4e3ad)


*Intervalos R-R.*


Para la parte del código lo que se implemento fue np.diff(tiempos_picos) lo que hace es calcular las diferencias entre tiempos consecutivos de los picos o los intervalos R-R en segundos, además tiempos_rr permite calcular el tiempo medio entre cada par de picos y así poder evidenciar en que instante ocurre cada intervalo. 


![image](https://github.com/user-attachments/assets/ec5fed8f-ef3c-42fe-90f6-09b24b30d838)


*Señal de los intervalos R-R obtenidos en el tiempo.*


Al tener una señal nueva compuesta por los valores de los intervalos R-R a lo largo del tiempo, puedes analizar la variabilidad en esos intervalos. Esta variabilidad se denomina HRV (Heart Rate Variability).
Este análisis es esencial porque refleja la actividad del sistema nervioso autónomo (SNA): Alta HRV= predominancia del sistema parasimpático (estado de relajación) y baja HRV = predominancia simpática (estrés, ansiedad).

Gracias a esta grafica evidenciamos que en el eje x se encuentra el tiempo en segundos que permite ver el momento del cálculo de un intervalo R-R o el tiempo entre dos latidos y en el eje y Intervalo R-R en segundos, es decir, cuánto tiempo pasó entre dos latidos consecutivos. Además nos permite ver qué mayor parte de la señal esta entre los 0.8 s y 1.1 s Esto indica una frecuencia cardíaca promedio entre aproximadamente, lo cual es un ritmo normal en reposo. Picos elevados cerca de 1.5 s aparecen dos valores aislados en los que el intervalo R-R sube a aproximadamente 1.5 segundos Esto puede deberse a una pausa sinusal (el corazón se detiene brevemente entre latidos) o un artefacto o error en la detección de los picos R (por ejemplo, un pico R omitido)o una respuesta vagal (parasimpática), que puede ralentizar el ritmo momentáneamente, por otro lado, hay pequeñas variaciones a lo largo del tiempo esto representa la variabilidad natural del ritmo cardíaco, que es normal y saludable o las variaciones más rápidas pueden estar relacionadas con la respiración (lo que se llama arritmia sinusal respiratoria).

Nosotros decidimos hacer una gráfica que muestre la frecuencia cardiaca estimada en función del tiempo que se obtiene a partir de los intervalos R-R. Esta visualización es una forma de analizar cómo varía la frecuencia de los latidos cardíacos a lo largo del registro.

![image](https://github.com/user-attachments/assets/c4857770-4699-486b-ad01-3e1aa7607f4e)


*Grafico de la frecuencia cardiaca basada en los intervalos R-R.*



Representa cómo varía la frecuencia cardíaca en el tiempo. Se observan: Variaciones normales (entre 55 y 70 bpm) en gran parte del tiempo, episodios con valores más altos (alrededor de 80 bpm), que podrían reflejar cambios fisiológicos que según nuestro diagrama de explicación sobre cómo se realizó el experimento donde se detecta esa elevación de la frecuencia cardiaca es cuando existió dicha activación del sistema simpático al someterla a estrés debido al juego y generarle presión por ganar y algunos picos inusuales, posiblemente causados por errores en la detección de picos R o artefactos de señal. Este análisis es bastante importante ya que permite observar el comportamiento del ritmo cardiaco a lo largo del tiempo, detecta fluctuaciones naturales del corazón debidas a la regulación autonómica e identificar eventos inusuales, como taquicardia (valores altos) o posibles fallos en la detección (valores extremos).

# Analisis de la HRV en el dominio del tiempo
La variabilidad de la frecuencia cardíaca (HRV) hace referencia a las variaciones temporales entre los latidos consecutivos del corazón, particularmente en los intervalos R-R, que se derivan de una señal de electrocardiograma (ECG).
En el ámbito temporal, el análisis implica la determinación de parámetros estadísticos básicos a partir de los intervalos R-R. Estos representan el balance entre la actividad simpática y parasimpática del sistema nervioso autónomo.
Se determinan dos parámetros fundamentales de HRV en el ámbito temporal:
RR Media: Costo medio entre los latidos. Ofrece una perspectiva del ritmo medio del corazón.
SDNN (Desviacion Normal de los intervalos NN): Se trata de la desviación estándar de los intervalos R-R (también conocidos como NN para "normal-anormal"). Representa la variabilidad global del ritmo del corazón. Se trata de un marcador relevante de la salud del sistema nervioso autónomo.
Estos dos valores sintetizan la variabilidad del ritmo cardíaco a lo largo del tiempo. Cuanto mayor sea la SDNN, más variabilidad existirá, lo que generalmente se asocia con una mejor salud cardiovascular y una mayor adaptabilidad fisiológica.

![image](https://github.com/user-attachments/assets/f21f0256-f50c-447b-8374-2412d03f02dc)

*HRV en el dominio del tiempo.*

Gracias a este código se obtiene la media y la desviación estándar de los intervalos R-R (SDNN) y además se realiza un histograma para evidenciar como está la distribución de los intervalos R-R para si mismo ver el grado de variabilidad en el tiempo. 

![image](https://github.com/user-attachments/assets/184775b9-528c-45e0-b214-e5c4370a4fe4)


*Resultados de media y desviación obtenidos.*

El valor de la media fue de 0.9900 s  esto indica que el corazón latió aproximadamente una vez cada 0.99 segundos y con una frecuencia de 60,6 lat/min indicando una frecuencia normal en reposo lo que nos permite ver que durante todo el experimento intervino más el sistema parasimpático puesto que no se logró llegar a los niveles de estrés deseados para que existiera un aumento mayor en la frecuencia cardiaca a pesar de que hubo picos no se evidencian del todo, por otro lado, el SDNN de 0.0945 s indicando que los intervalos R-R varían en promedio 94.5 ms, indicando una variabilidad saludable reflejando una buena regulación autónoma ya que se encontró en reposo durante los primeros 3 minutos de experimento y al final fue cuando se detectó una activación simpática, pero que en nuestro caso no fue muy relevan te porque no se vio muy reflejada en los resultados. 

![image](https://github.com/user-attachments/assets/93e35392-48a3-4304-881b-85bfd14040da)


*Histograma de intervalos R-R.*


El histograma de intervalos R-R revela que la mayoría de los valores se agrupan entre 0.95 y 1.05 segundos, con un máximo de 1.0 s aproximadamente, lo que se alinea con una media RR de 0.9900 s e indica un ritmo cardíaco estable y regular. La distribución es un poco asimétrica hacia la derecha (sesgo positivo), a causa de ciertos valores dispersos entre 1.4 y 1.6 s, lo que es habitual en señales fisiológicas reales debido a posibles interrupciones sinusales, artefactos o fluctuaciones en la respiración. Estos valores extremos, a pesar de ser escasos, no influyen de manera significativa en la media, pero sí aportan a la dispersión global que se observa en el estudio de la variabilidad o también cabe la posibilidad que sea un poco de activación mínima simpática detectada al final puesto que en ese tiempo era cuando ella estaba sometida a estrés o a actos que aumentaran su frecuencia cardiaca.

*Aplicación de transformada Wavelet*
La transformada wavelet estacionaria (SWT) con Daubechies 4 (db4) se usa para analizar cómo varían las frecuencias del ritmo cardíaco (HRV) a lo largo del tiempo. Esto permite:

Separar las señales en diferentes bandas de frecuencia (baja y alta).

Observar la actividad simpática y parasimpática, ya que:

Las frecuencias bajas (LF) están asociadas a la actividad simpática.

Las frecuencias altas (HF) están asociadas a la actividad parasimpática.

Detectar cambios en la potencia espectral en momentos específicos, lo que ayuda a entender cómo responde el sistema nervioso autónomo ante estímulos o condiciones fisiológicas.

![image](https://github.com/user-attachments/assets/d576008f-118d-4883-b0c0-1feb03a5b355)

Se escogio utilizar esta señal ya que para realizar este espectrograma es necesario usar los r-r calculados con anterioridad y esta tienen la diferencia de ser discreta a diferencia de la señal extraía directamente que es continua. Al ser una señal discreta es necesario una función de wavelet que comparta esta característica además de ser útil para señales fisiológicas. Con estos puntos se decidió que la función que cumplía estas características es la daubechie ya es común utilizarla en ecg además de ser una función discreta ideal para este laboratorio.


Para comenzar se preparar la señal para la Transformada Wavelet Estacionaria (SWT). Descomponiendo la señal en 4 niveles de wavelet y se calcula el tamaño de bloque para cada nivel. Ademas se lee la cantidad de muestras de la señal interpolada de los intervalos R-R. Y como ultimo se crea niveles de wavelet y se calcula el tamaño de bloque para cada nivel. Ademas se crea el eje de tiempo correspondiente.
![image](https://github.com/user-attachments/assets/00f21516-1490-49b6-889b-8edc7e0e80d1)

SE definiendo la wavelet que se usaria siendo la daubechie, y de paso definiendo los niveles que se utilizaron. Se aplico  la Transformada Wavelet Discreta Estacionaria (SWT).

A diferencia de la transformada wavelet discreta estándar (DWT), la SWT no cambia la longitud de la señal y mantiene alineadas las características en el tiempo, lo que es útil para análisis como el espectrograma.

![image](https://github.com/user-attachments/assets/431d58e6-711a-43d6-9a0d-a35d930bc2fd)

Se extraen los coeficientes de detalle para graficar.

![image](https://github.com/user-attachments/assets/f42e9f63-b747-4220-a65e-7a8322799c69)

Por ultimo se grafica.

![image](https://github.com/user-attachments/assets/b83982ff-1dda-4775-8959-f6c89a637bdb)

Como resultado de este proceso se obtuvo este espectrograma.

![image](https://github.com/user-attachments/assets/fa9cc19b-2e3d-427c-b924-1e26269f5e34)

Este escalograma muestra cómo varía la potencia espectral del ritmo cardíaco a lo largo del tiempo, distribuida en 4 niveles de descomposición mediante la transformada wavelet estacionaria con Daubechies 4.

🔹 1. Banda de baja frecuencia (LF) – Niveles 3 y 4.
Se aprecian claramente zonas de color amarillo a rojo —indicadoras de alta potencia— concentradas en los niveles 3 y 4, que cubren la banda de baja frecuencia (0.04–0.15 Hz). Estas elevadas intensidades espectrales señalan episodios de predominio simpático en momentos específicos del registro por ejemplo, alrededor de los 100–110 s, 180–210 s y próximos a los 300 s, lo que sugiere que en esas ventanas temporales el sistema nervioso autónomo se encontraba más activado bajo un perfil simpático. La sucesión de estos picos de potencia a lo largo del tiempo revela, además, fluctuaciones dinámicas del tono simpático que podrían corresponder a respuestas fisiológicas o emocionales variables durante la prueba.

🔹 2. Banda de alta frecuencia (HF) – Nivel 2.
Por otro lado, el nivel 2, correspondiente a la banda de alta frecuencia (0.15–0.4 Hz) y asociado a la actividad parasimpática, muestra una potencia moderada (verde-amarilla) en ciertos intervalos. Este patrón indica una modulación vagal intermitente por ejemplo, relacionada con ciclos respiratorios o fases de relajación que, aunque menos intensa que la LF, confirma la presencia de influencias parasimpáticas en el control del ritmo cardíaco a lo largo del tiempo.

El espectrograma muestra la variabilidad de los intervalos R–R, El color (rojo/amarillo) indica mucha energía o potencia en esa banda de frecuencia (LF o HF) en ese momento. Y traza la variabilidad de los intervalos R–R a esas frecuencias. La activación simpática suele reducir la variabilidad (disminuye el poder en bandas, sobre todo en HF), y al mismo tiempo aumenta la frecuencia media de latidos.
Por ello, un pico rojo en LF indica más potencia en modulaciones lentas (0.04–0.15 Hz), asociadas a la influencia simpática/vagal, pero no significa necesariamente que el corazón esté latiendo más rápido en ese instante: significa que la variabilidad a esas escalas es mayor.

# Preguntas clave.
1. ¿Qué diferencias se observan entre los análisis en el dominio del tiempo y el dominio tiempo-frecuencia?

Al contrastar la distribución temporal de las frecuencias adquiridas a través de la transformada wavelet con los parámetros temporales (como la media RR y el SDNN), se puede percibir una correlación adicional entre ambas representaciones del estudio de la variabilidad de la frecuencia cardíaca (HRV). Aunque los parámetros del dominio temporal representan la variabilidad global del ritmo cardíaco por ejemplo, un valor de SDNN superior sugiere mayor variabilidad y, por ende, un mejor equilibrio autonómico, la transformada wavelet facilita la descomposición de la señal en distintas bandas de frecuencia a través del tiempo, ofreciendo datos más precisos acerca de cómo cambia la actividad simpática y parasimpática en momentos concretos.
El rango de frecuencia baja (LF, normalmente entre 0.04 y 0.15 Hz) se relaciona con una mezcla de actividad simpática y parasimpática, aunque se percibe como un indicador más indirecto del tono simpático. En cambio, la banda de alta frecuencia (HF, 0.15–0.4 Hz) tiene una relación más íntima con la actividad parasimpática, en particular con la modulación vagal del ritmo cardíaco. Un incremento en la potencia de la banda HF sugiere una mayor actividad parasimpática (relajación, reposo), mientras que un incremento en la LF podría sugerir activación simpática (estrés, esfuerzo), aunque esto varía según el entorno fisiológico.
En nuestro caso como se nota un incremento momentáneo en la potencia de la banda HF en la transformada wavelet, indica una etapa de relajación que también se manifeste como una reducción de la frecuencia cardíaca (incremento de RR) o una mayor estabilidad en la señal (disminución de SDNN). En cambio, un aumento en la potencia LF esta relacionado con una mayor variabilidad en los intervalos R-R (mayor SDNN) o con episodios de activación fisiológica. En conclusión, ambos métodos —temporal y frecuencial— se complementan: el dominio temporal proporciona una perspectiva global de la variabilidad, mientras que el análisis wavelet muestra cuándo se producen las variaciones en la modulación autonómica.


2. ¿Qué efecto tiene el uso de diferentes funciones wavelet en los resultados del análisis?


   
La selección de la función wavelet influye de manera directa en la resolución temporal y frecuencial del estudio. En tu situación, se empleó la wavelet Daubechies 4 (db4), la cual es apropiada para señales fisiológicas como el ECG por su excelente ubicación temporal y su habilidad para identificar transiciones rápidas. Si se optara por una wavelet con más momentos de desvanecimiento o más simétrica (como symlets o coiflets), podría optimizar la separación de componentes de frecuencia reducida o producir una representación más fluida, aunque a cambios bruscos. Así, es necesario ajustar la función wavelet al tipo de análisis que se quiere priorizar (precisión temporal o frecuencial).


3. ¿Qué aplicaciones reales tiene esta práctica?



El estudio de la HRV tiene usos clínicos y deportivas fundamentales. En el ámbito médico, facilita la identificación de problemas autonómicos en pacientes con afecciones cardiovasculares, diabetes o desórdenes neurológicos, al mostrar cambios en la dinámica simpática y parasimpática. En áreas como el deporte y la psicología, contribuye a supervisar el estrés, la recuperación y la carga de entrenamiento a través de la observación de cambios en vivo. Además, estos estudios son esenciales en contextos de biofeedback y control adaptable en aparatos médicos, tales como marcapasos inteligentes o exoesqueletos rehabilitadores que se adaptan a la situación del paciente en tiempo real.







































