# Agente-Inteligente-para-la-Seguridad-en-Condominios


1. Descripcion del problema:

Este proyecto consiste en el diseño y desarrollo de un agente inteligente de seguridad orientado a la gestión automatizada de la seguridad en un condominio. El agente combina técnicas de reconocimiento facial, de modelo de entrenamiento y de un modelo de aprendizaje supervisado para asistir en la vigilancia, el control de accesos y la respuesta ante eventos sospechosos.


2. Estado del arte breve: 

Ampliamos la base de datos de rostros con imágenes de bases de datos públicas de personas conocidas y entrenamos el modelo mediante Roboflow utilizando cientos de fotos para cada rostro. Para entrenar el modelo, dividimos la base de datos de cada rostro en 70% para entrenamiento, 20% para validación y 10% para pruebas.


3. Objetivos del proyecto:

- Implementar un agente inteligente capaz de monitorear en tiempo real entradas y zonas comunes mediante cámaras.

- Automatizar el control de acceso de residentes y visitantes usando reconocimiento facial o validación de datos.

- Detectar comportamientos o situaciones anómalas o sospechosas (como intrusos o movimientos fuera del horario permitido).

- Emitir alertas inteligentes al personal de seguridad o residentes mediante un sistema de notificación.


4. Arquitectura del agente o sistema:

La arquitectura del sistema del agente inteligente de seguridad esta organizado en distintas partes, la primera es la parte de la captura de rostro por el cual el agente funciona con un modulo de percepcion segun el cual recibe y procesa informacion del entorna via las camaras y sensores. La segunda parte del agente es el algoritmo del reconocimiento facial que funciona con YOLO y captura rostro para comparar con la base de datos. El entrenamiento del agente se hace en Roboflow con rostros y datos pre entrenados. Finalmente se guarda en un archivo Excel los reconocimientos del agente con el nombre y la hora de la deteccion.


5. Algoritmo de Machine Learning utilizado y su justificación:

- 1) YOLOv8 (You Only Look Once) - Detección de Objetos
  
Tipo de algoritmo: Algoritmo de Deep Learning (Específicamente, una red neuronal convolucional de detección de objetos)

Descripción:

YOLOv8 es un modelo basado en redes neuronales convolucionales (CNN) que se utiliza para la detección de objetos en imágenes o videos en tiempo real. A diferencia de otros enfoques que primero identifican áreas de interés y luego hacen la clasificación (como R-CNN o Fast R-CNN), YOLO procesa toda la imagen de una sola vez y predice las cajas delimitadoras (bounding boxes) y las clases de objetos dentro de esas cajas. Esto lo hace muy rápido y eficiente para aplicaciones en tiempo real.

Justificación del uso:

Eficiencia y velocidad: YOLO es muy popular porque es rápido y puede realizar predicciones en tiempo real, lo cual es esencial para aplicaciones como la detección de personas en cámaras en vivo.

Precisión: Es eficaz para detectar y clasificar múltiples objetos en una sola pasada.

Aplicación en este código: En el código, se utiliza YOLOv8 para detectar personas en un flujo de video en tiempo real, lo cual es esencial para la tarea de monitoreo y registro de personas.

- 2) LBPH (Local Binary Pattern Histogram) - Reconocimiento Facial

Tipo de algoritmo: Algoritmo de Machine Learning supervisado para reconocimiento facial.

Descripción:

LBPH es un algoritmo de aprendizaje supervisado que se utiliza comúnmente para reconocimiento facial. Su funcionamiento se basa en el análisis de patrones locales binarios (LBP) en las imágenes faciales. En términos simples, el LBP analiza la textura de una imagen dividiéndola en pequeñas regiones y comparando los píxeles vecinos para generar un descriptor único que representa las características de la textura local. Luego, se calcula un histograma de los patrones encontrados y se utiliza para representar la imagen de la cara. En la fase de entrenamiento, el algoritmo crea un modelo que aprende a asociar cada patrón de rostro con una etiqueta (persona), y en la fase de predicción, compara un rostro desconocido con el modelo previamente entrenado para identificar a la persona.

Justificación del uso:

Eficiencia y baja carga computacional: Aunque los métodos modernos como las redes neuronales profundas (DNN) son más precisos, LBPH es más ligero y rápido, lo que lo hace adecuado para aplicaciones donde el tiempo de respuesta es crucial y los recursos computacionales limitados.

Simplicidad y robustez: LBPH es relativamente sencillo de implementar y ha demostrado ser bastante robusto incluso en condiciones de variabilidad en la iluminación, pose y expresión facial.

Aplicación en este código: En el código, LBPH se utiliza para realizar reconocimiento facial en las caras detectadas por YOLOv8. El modelo LBPH asigna un nombre a la persona según las imágenes previamente registradas en un conjunto de entrenamiento.

- 3) Justificación Global para el Uso Combinado de YOLO y LBPH
YOLO para detección de objetos y LBPH para reconocimiento facial se combinan perfectamente para una aplicación robusta de reconocimiento de personas en tiempo real:

Detección inicial con YOLOv8: Primero, YOLOv8 se encarga de detectar a las personas en cada fotograma de video. Esto permite que el sistema se enfoque solo en las áreas que contienen personas, eliminando la necesidad de procesar el resto de la imagen.

Reconocimiento facial con LBPH: Una vez que YOLO ha localizado a una persona, se utiliza LBPH para identificarla a partir de una base de datos de rostros previamente entrenados. Esto proporciona una identificación precisa dentro de las personas detectadas por YOLO.

Sinergia entre YOLO y LBPH: Esta combinación es eficaz porque YOLO se encarga de la localización rápida y LBPH realiza la identificación precisa una vez que la persona ha sido detectada. Esta es una estrategia común en sistemas de reconocimiento facial de alto rendimiento.

Resumen de los Algoritmos de Machine Learning Utilizados
YOLOv8: Algoritmo de Deep Learning para detección de objetos (personas).

Justificación: Rápido, preciso, adecuado para procesar imágenes en tiempo real.

LBPH (Local Binary Pattern Histogram): Algoritmo de Machine Learning supervisado para reconocimiento facial.

Justificación: Ligero, eficiente, fácil de implementar y adecuado para sistemas con requisitos de procesamiento moderados.

- 4) Conclusión
El código utiliza YOLOv8 para realizar la detección de objetos en imágenes, específicamente para identificar personas en tiempo real, y LBPH para reconocer a esas personas basándose en las características faciales extraídas de las imágenes. Esta combinación de técnicas permite realizar un sistema robusto y eficiente para la detección e identificación facial en tiempo real.


6. Tecnologías y librerías empleadas:

Librerías y Tecnologías Empleadas en el Código de Detección de Objetos con YOLOv8 y Reconocimiento Facial con LBPH:

Librerías Principales:

- 1) OpenCV (cv2):

Tecnología: Librería de visión por computadora y procesamiento de imágenes en Python.

Propósito: Se usa para trabajar con imágenes y videos en tiempo real. En este caso:

Captura de imágenes desde la cámara con cv2.VideoCapture().

Procesamiento de imágenes para detección de objetos y reconocimiento facial.

Conversión de imágenes a escala de grises con cv2.cvtColor().

Redimensionamiento de imágenes con cv2.resize().

Dibujo de cajas delimitadoras y texto sobre las imágenes.

Guardado de resultados en archivos de Excel.

- 2) Ultralytics YOLO (ultralytics.YOLO):

Tecnología: Implementación moderna de YOLOv8 para detección de objetos.

Propósito: Utiliza el modelo YOLOv8 preentrenado para detectar objetos en tiempo real (en este caso, personas).

Permite cargar el modelo entrenado (YOLO('best.pt')) y hacer inferencias sobre imágenes o videos para obtener las predicciones de las cajas delimitadoras de objetos.

- 3) OpenPyXL:

Tecnología: Librería para leer y escribir archivos de Excel en Python.

Propósito: Se usa para guardar el historial de detecciones en un archivo Excel.

Permite registrar el nombre de las personas detectadas y la hora de la detección en una hoja de cálculo.

- 4) Winsound: 

Tecnología: Módulo estándar de Python para reproducir sonidos en Windows.

Propósito: Se utiliza para generar una alerta sonora (winsound.Beep()) cada vez que se detecta una persona en el video en tiempo real.

- 5) Numpy:

Tecnología: Librería para cálculos numéricos en Python.

Propósito: Se utiliza principalmente para trabajar con arreglos numéricos, como la lista de etiquetas en el reconocimiento facial y la manipulación de datos.

- 6) Datetime:

Tecnología: Módulo de Python para manipulación de fechas y horas.

Propósito: Se usa para registrar la hora exacta de cada detección, lo cual es importante para la funcionalidad de control del tiempo entre detecciones repetidas de una misma persona.

- 7) OS:

Tecnología: Módulo de Python que proporciona una interfaz para interactuar con el sistema operativo.

Propósito: Se usa para trabajar con rutas de archivos y directorios, como cargar imágenes desde carpetas específicas y gestionar archivos de Excel.

- 8) Cv2.face.LBPHFaceRecognizer_create():

Tecnología: Parte de la librería OpenCV para reconocimiento facial.

Propósito: Se utiliza para crear un reconocedor facial basado en el algoritmo LBPH (Local Binary Pattern Histogram).

El modelo entrenado se usa para identificar personas a partir de sus características faciales.

  2. Detalles Técnicos de las Tecnologías Usadas:

Tecnologías de Machine Learning y Deep Learning:

- 1) YOLO (You Only Look Once):

Tecnología: Deep Learning (Red Neuronal Convolucional - CNN).

Modelo Utilizado: YOLOv8 (una versión más reciente y optimizada del algoritmo YOLO).

Uso: Detección de objetos en imágenes y videos en tiempo real. En este caso, se usa para detectar personas en las imágenes obtenidas de la cámara.

- 2) LBPH (Local Binary Pattern Histogram):

Tecnología: Machine Learning supervisado.

Modelo Utilizado: LBPH para el reconocimiento facial.

Uso: Un algoritmo que se utiliza para identificar personas a partir de sus rostros mediante patrones de textura local en las imágenes faciales.

  3. Otras Tecnologías Utilizadas:

- 1) Excel (Excel/CSV para el registro de detecciones):

Tecnología: Microsoft Excel o archivos CSV para almacenar los registros de detección.

Librería utilizada: OpenPyXL para leer y escribir los datos de detección (nombre de la persona y la hora) en un archivo Excel.

- 2) Sistema Operativo (Windows):

Tecnología: El código hace uso de Windows específicamente con la librería winsound para emitir sonidos y alertas.

- 3) IDE (Entorno de desarrollo):

No se menciona explícitamente, pero este tipo de código generalmente se ejecuta en un entorno como Jupyter Notebook, VS Code o PyCharm para facilitar la depuración y visualización de los resultados.

Resumen de Tecnologías y Librerías Empleadas:

- OpenCV (cv2): Procesamiento de imágenes, detección de objetos, dibujo de cajas y texto, captura de imágenes desde la cámara.

- YOLOv8 (ultralytics.YOLO): Detección de objetos en tiempo real utilizando un modelo preentrenado.

- OpenPyXL: Lectura y escritura de archivos Excel para registrar las detecciones.

- Numpy: Manipulación de datos numéricos para el manejo de las etiquetas de reconocimiento facial.

- Winsound: Emisión de alertas sonoras en Windows.

- Datetime: Registro de la hora exacta de cada detección.

- OS: Manejo de rutas de archivos y directorios.


7. Instrucciones claras para instalar dependencias y ejecutar el proyecto:

Para ejecutar el proyecto deberia tener instaladas las liberias utilizadas y el modelo en local con la base de datos compilada en Roboflow.

8. Parámetros principales de entrenamiento y métricas de evaluación:

Entrenamiento de YOLO para Reconocimiento Facial con Roboflow:

  1. ¿Qué es Roboflow?

Roboflow es una plataforma que facilita la creación, gestión y entrenamiento de modelos de detección de objetos. Permite cargar imágenes, anotarlas, y entrenar modelos utilizando frameworks de deep learning como YOLO, TensorFlow, y PyTorch. Es una excelente herramienta para gestionar y entrenar modelos personalizados sin tener que escribir todo el código desde cero.

  3. Base de Datos con Rostros de Personas Famosas
     
En este caso, tenemos una base de datos que contiene imágenes de rostros de personas famosas. Estas imágenes son las que usamos para entrenar el modelo de detección facial. Cada imagen está etiquetada con el nombre de la persona para que el modelo pueda aprender a asociar la cara con su identidad.

Pasos del proceso:

- 1) Subir las imágenes a Roboflow:

Subimos las imágenes de las personas famosas a Roboflow. Durante el proceso de subida, Roboflow nos permite etiquetar las imágenes, es decir, dibujar cajas delimitadoras alrededor de los rostros en las fotos y etiquetar esos rostros con los nombres de las personas.

- 2) Anotación de las Imágenes:

Las imágenes necesitan ser anotadas correctamente para que el modelo aprenda a detectar los rostros. Roboflow tiene herramientas integradas para realizar este proceso de anotación de manera sencilla. Para cada rostro en la imagen, se dibuja una caja de delimitación (bounding box) y se asigna una etiqueta con el nombre de la persona famosa (por ejemplo, "Nelson", "Emma Watson", etc.).

- 3) División de la Base de Datos:

Roboflow ofrece la capacidad de dividir automáticamente las imágenes en tres conjuntos:
Entrenamiento (70%): El modelo se entrena con estas imágenes para aprender a identificar los rostros. Validación (20%): Este conjunto se utiliza para validar el rendimiento del modelo durante el entrenamiento y ajustarlo si es necesario. Pruebas (10%): Este conjunto se utiliza después del entrenamiento para evaluar el rendimiento final del modelo. Esta división es crucial para evitar el overfitting (cuando el modelo se ajusta demasiado a los datos de entrenamiento y pierde capacidad de generalización) y asegurar que el modelo no solo funciona bien en los datos de entrenamiento, sino también en nuevos datos.

- 4) Entrenamiento del Modelo con YOLO:

Una vez que las imágenes están anotadas y la base de datos está dividida, Roboflow nos permite entrenar un modelo de YOLO para la detección de objetos. En este caso, el modelo YOLOv8 es ideal para este tipo de tarea debido a su eficiencia y rapidez en la detección de objetos en imágenes en tiempo real. Después de entrenar el modelo, Roboflow nos da un archivo con los pesos del modelo (por ejemplo, best.pt), que es lo que luego cargamos en nuestro código para hacer predicciones sobre nuevas imágenes o videos. 


9. Resultados obtenidos y breve discusión:

En este proyecto de reconocimiento facial, hemos explorado e implementado una solución basada en el modelo YOLOv8 para detectar y reconocer rostros en tiempo real utilizando una cámara. Sin embargo, durante las pruebas iniciales, nos encontramos con algunas dificultades relacionadas con el reconocimiento preciso de los rostros, especialmente cuando intentábamos reconocer nuestros propios rostros al utilizar el programa directamente con nuestras cabezas frente a la cámara. De hecho, el reconocimiento facial en tiempo real, cuando se aplica directamente a los rostros de las personas, sigue siendo un desafío complejo debido a diversos factores. Entre los principales problemas que afectan la precisión del modelo se incluyen las variaciones en las condiciones de iluminación, los ángulos de visión, las expresiones faciales cambiantes, así como la calidad de la cámara utilizada. Como resultado, el modelo de detección facial, aunque efectivo en muchas circunstancias, muestra ciertas limitaciones cuando se enfrenta a estos factores. No obstante, el entrenamiento del modelo utilizando una base de datos de Roboflow ha permitido mejorar significativamente la precisión del sistema. Gracias al entrenamiento con una base de datos bien estructurada y diversa, hemos logrado obtener una precisión media por clase que oscila entre el 96% y el 100%. Esto demuestra que, cuando el modelo se entrena con una base de datos optimizada y se ajusta correctamente a las condiciones de los rostros que se espera reconocer, el rendimiento del sistema puede ser extremadamente alto.


10. Conclusiones principales:

En resumen, aunque la implementación directa con rostros individuales en condiciones no controladas presenta algunos desafíos, el uso de una base de datos de Roboflow ha permitido mejorar considerablemente la precisión del modelo. Esto sugiere que, con un entrenamiento adecuado y una base de datos bien gestionada, los sistemas de reconocimiento facial pueden ofrecer un rendimiento sobresaliente en aplicaciones más controladas y específicas.


11. Referencias si se usaron recursos externos:

OpenAI.
