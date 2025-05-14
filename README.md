# Agente-Inteligente-para-la-Seguridad-en-Condominios

1. Descripcion del problema:

Este proyecto consiste en el diseño y desarrollo de un agente inteligente de seguridad orientado a la gestión automatizada de la seguridad en un condominio. El agente combina técnicas de reconocimiento facial, de modelo de entrenamiento y de un modelo de aprendizaje supervisado para asistir en la vigilancia, el control de accesos y la respuesta ante eventos sospechosos.

2. Estado del arte breve: 

Ampliamos la base de datos de rostros con imágenes de bases de datos públicas de personas conocidas y entrenamos el modelo mediante Robotflow utilizando cientos de fotos para cada rostro. Para entrenar el modelo, dividimos la base de datos de cada rostro en 70% para entrenamiento, 20% para validación y 10% para pruebas.

3. Objetivos del proyecto:

- Implementar un agente inteligente capaz de monitorear en tiempo real entradas y zonas comunes mediante cámaras.

- Automatizar el control de acceso de residentes y visitantes usando reconocimiento facial o validación de datos.

- Detectar comportamientos o situaciones anómalas o sospechosas (como intrusos o movimientos fuera del horario permitido).

- Emitir alertas inteligentes al personal de seguridad o residentes mediante un sistema de notificación.

4. Arquitectura del agente o sistema:

La arquitectura del sistema del agente inteligente de seguridad esta organizado en distintas partes, la primera es la parte de la captura de rostro por el cual el agente funciona con un modulo de percepcion segun el cual recibe y procesa informacion del entorna via las camaras y sensores.

La segunda parte del agente es el algoritmo del reconocimiento facial que funciona con YOLO y captura rostro para comparar con la base de datos.

El entrenamiento del agente se hace en Robotflow con rostros y datos pre entrenados.

Finalmente se guarda en un archivo Excel los reconocimientos del agente con el nombre y la hora de la deteccion.

6. Algoritmo de Machine Learning utilizado y su justificación:

7. Tecnologías y librerías empleadas:

8. Instrucciones claras para instalar dependencias y ejecutar el proyecto:

9. Parámetros principales de entrenamiento y métricas de evaluación:

10. Resultados obtenidos y breve discusión:

11. Conclusiones principales:

12. Referencias si se usaron recursos externos:


