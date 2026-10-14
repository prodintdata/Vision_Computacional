# Análisis Comparativo: Modelo Baseline (Denso) vs. CNN (Green AI)

Este informe presenta la evaluación comparativa entre el modelo baseline (completamente denso) y la Red Neuronal Convolucional (CNN) entrenados sobre el conjunto de datos **Fashion-MNIST** utilizando 8 épocas en un entorno de CPU.

---

## 1. Comparación de F1 Macro y Métricas por Clase
* **Modelo Denso (Baseline):** F1 macro de **$0.8638$**.
* **Red CNN:** F1 macro de **$0.7891$**.
* **Lectura:** En esta ejecución con 8 épocas, el modelo denso superó ligeramente al modelo CNN en la métrica global F1 macro. Esto demuestra que las capas densas simples pueden capturar relaciones globales rápidamente en imágenes de baja resolución ($28 \times 28$), mientras que las arquitecturas convolucionales pueden requerir más épocas o ajustes de hiperparámetros para explotar todo su potencial espacial.

---

## 2. Cantidad de Parámetros y Completa Estructura
* **Modelo Denso:** $50,890$ parámetros.
* **Red CNN:** $19,466$ parámetros.
* **Lectura:** A pesar de ser más compleja conceptualmente, la CNN utiliza **menos de la mitad de parámetros** que el modelo denso. Las operaciones de convolución y *pooling* reducen drásticamente la dimensionalidad de entrada antes de llegar a las capas de clasificación.

---

## 3. Tiempo de Inferencia
* **Modelo Denso:** $\approx 0.047 \text{ ms/imagen}$.
* **Red CNN:** $\approx 0.222 \text{ ms/imagen}$.
* **Lectura:** El modelo denso realiza una inferencia más rápida por imagen debido a la simplicidad de sus multiplicaciones matriciales directas, en contraste con el procesamiento por filtros espaciales de la CNN.

---

## 4. Perspectiva Green AI: ¿La mejora justifica el costo?
Bajo los principios de **Green AI**, la eficiencia computacional y el impacto energético son tan importantes como la precisión predictiva:
1. **Costo de Entrenamiento:** El modelo denso entrenó en apenas $\approx 9$ segundos, mientras que la CNN requirió $\approx 290$ segundos en el mismo entorno de CPU.
2. **Conclusión:** Aunque la CNN ofrece una arquitectura más elegante y compacta en cuanto al número de parámetros, el modelo denso baseline demostró ser más eficiente tanto en tiempo de entrenamiento como en rendimiento global ($F1 = 0.8638$) para este escenario específico. Por lo tanto, bajo restricciones de recursos y criterios de sostenibilidad, el baseline representa una solución sumamente competitiva.