# Laboratorio-5_PDS

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









