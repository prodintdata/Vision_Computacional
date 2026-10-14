# Model Card - Fashion-MNIST CNN

## Modelo y versión
* **Arquitectura:** Red Neuronal Convolucional (CNN) comparada con un modelo Baseline Denso.
* **Versión:** 1.0 (Laboratorio 07 - Visión Computacional).
* **Framework:** TensorFlow / Keras (Python 3.12).

## Uso previsto
* Propósito académico y didáctico para la clasificación de imágenes en escala de grises de prendas de vestir pertenecientes al dataset Fashion-MNIST ($28\times28$ píxeles, 10 clases).
* Introducción a la evaluación de modelos de aprendizaje profundo bajo restricciones de recursos de hardware.

## Usos fuera de alcance
* No está diseñado ni validado para su uso en entornos de producción críticos.
* Estrictamente fuera de alcance para dominios médicos (diagnóstico por imagen), sistemas de lectura OCR de alta precisión, control de calidad industrial automatizado de alta exigencia, o sistemas de vigilancia/seguridad.

## Dataset y particiones
* **Dataset:** Fashion-MNIST.
* **Particiones:** 60,000 imágenes de entrenamiento y 10,000 imágenes de prueba (test set).
* **Preprocesamiento:** Normalización de los valores de los píxeles al rango $[0, 1]$ dividiendo por 255.0.

## Métricas globales y por clase
* **Exactitud global (Accuracy):** 79.3% ($0.793$)
* **F1-Score Macro:** 0.789
* **Métricas detalladas por clase (Precision / Recall / F1-score):**
  * Clase 0 (T-shirt/top): Precisión: 0.645 | Recall: 0.807 | F1: 0.717
  * Clase 1 (Pantalón): Precisión: 0.988 | Recall: 0.932 | F1: 0.959
  * Clase 2 (Pullover): Precisión: 0.707 | Recall: 0.641 | F1: 0.672
  * Clase 3 (Vestido): Precisión: 0.754 | Recall: 0.844 | F1: 0.797
  * Clase 4 (Abrigo): Precisión: 0.660 | Recall: 0.663 | F1: 0.661
  * Clase 5 (Sandalia): Precisión: 0.950 | Recall: 0.885 | F1: 0.916
  * Clase 6 (Camisa): Precisión: 0.498 | Recall: 0.373 | F1: 0.427
  * Clase 7 (Zapatilla): Precisión: 0.855 | Recall: 0.952 | F1: 0.901
  * Clase 8 (Bolso): Precisión: 0.917 | Recall: 0.936 | F1: 0.926
  * Clase 9 (Botín): Precisión: 0.935 | Recall: 0.896 | F1: 0.915

## Comparación de costo (Green AI) y Entorno
* **Hardware:** GitHub Codespaces (Entorno basado en CPU, sin aceleración CUDA/GPU activa).
* **Parámetros del modelo CNN:** 19,466 parámetros entrenables (frente a 50,890 del Baseline Denso).
* **Tiempo de entrenamiento (8 épocas):** ~290 segundos en CPU.
* **Tiempo de inferencia:** ~0.22 ms por imagen.

## Limitaciones y riesgos
* **Ambigüedad morfológica:** La mayoría de los errores se concentran en prendas del tren superior (abrigos, camisas, vestidos y pulóveres) debido a la baja resolución de $28\times28$ píxeles y la similitud en sus texturas y siluetas.
* **Restricción de hardware:** El entrenamiento en CPU limita la escalabilidad a arquitecturas más profundas o datasets de mayor resolución sin un tiempo de cómputo elevado.

## Supervisión y monitoreo
* Se requiere supervisión humana constante ante cualquier intento de aplicar este modelo fuera de su entorno estrictamente didáctico. No debe automatizarse la toma de decisiones basada en sus predicciones debido a los márgenes de error observados en clases visualmente similares.