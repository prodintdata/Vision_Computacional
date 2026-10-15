# Reporte: Clasificador Visual con CNN y Model Card (U02.E04)

**Asignatura:** INF-8239 Ciencia de Datos II  
**Unidad 02:** Visión Computacional  
**Mandato:** Clasificador visual con CNN y Model Card  
**Autor:** Jhonatan Leandro Cabral Pujols  
**Código:** U02.E04  
**Evidencias:** LAB07  

---

## 1. Auditoría, Partición Reproducible y Entorno
El proyecto se diseñó bajo estrictos estándares de reproducibilidad utilizando herramientas modernas de gestión de dependencias (`uv`) y especificaciones fijadas en `pyproject.toml` y `uv.lock`. Es compatible con Python 3.12 y TensorFlow 2.21, soportando ejecución tanto en entornos de CPU (GitHub Codespaces) como con aceleración por GPU (Google Colab) mediante dependencias opcionales. En el script de entrenamiento (`scripts/train_cv.py`), se fijó la semilla global `SEED = 42` y se activaron las operaciones deterministas de TensorFlow (`TF_DETERMINISTIC_OPS = "1"`). El dataset Fashion-MNIST fue normalizado dividiendo los píxeles entre 255.0 (mapeados al rango $[0, 1]$) y particionado en 60,000 muestras de entrenamiento, 6,000 muestras de validación y 10,000 muestras de prueba (`test set`).

---

## 2. Baseline y Dos Arquitecturas Funcionales
Se implementaron y compararon dos arquitecturas secuenciales de Keras mediante funciones de factoría modular ubicadas en `src/inf8239_u02_cv/models.py`. 

### Tabla comparativa de desempeño y costos (`cv_metrics.json`):

| Modelo / Arquitectura | Estrategia o Parámetros | F1 Macro | Estado / Persistencia |
| :--- | :--- | :---: | :--- |
| **dense** (Baseline Denso) | 50,890 parámetros, Flatten + Dense(64) | 0.8638 | Baseline comparativo primario |
| **cnn** (Red Convolucional) | 19,466 parámetros, Conv2D + Pooling + GlobalAvg | 0.7891 | Seleccionado (`models/best_cnn.keras`) |

Ambos modelos se compilaron con el optimizador Adam ($	ext{learning rate} = 0.001$) y pérdida `sparse_categorical_crossentropy`. Se integró `EarlyStopping` (paciencia de 2 épocas restaurando los mejores pesos) y `ModelCheckpoint` para persistir el mejor modelo de la CNN.

---

## 3. Métricas, Curvas y Errores por Clase
La evaluación sobre el conjunto de prueba (10,000 imágenes) arrojó una exactitud del 79.3% ($0.793$) y un puntaje $F1	ext{-macro}$ de $0.789$ para la CNN. A partir de la matriz de confusión (`reports/confusion_cnn.png`) y el panel visual de errores (`reports/cnn_errors.png`), se identificaron hallazgos clave:
* **Aciertos sólidos:** Desempeño sobresaliente en clases geométricamente definidas como la Clase 1 (Pantalón) con 932 aciertos y la Clase 7 (Zapatilla) con 952 aciertos.
* **Zonas de confusión:** La Clase 4 (Abrigos/Coats) concentra la mayor cantidad de errores, siendo confundida erróneamente con pulóveres (Clase 2) o camisas (Clase 6).
* **Causa raíz:** La alta superposición morfológica y similitud de texturas en prendas del tren superior bajo la baja resolución de $28 	imes 28$ píxeles.

---

## 4. Costo, Tamaño y Decisión Técnica
Bajo los principios de **Green AI** y eficiencia computacional, se evaluaron los costos: el modelo denso entrenó en aproximadamente 9.16 segundos y requirió 50,890 parámetros, con una velocidad de inferencia de 0.047 ms/imagen. La CNN requirió 290.01 segundos de entrenamiento en CPU y 19,466 parámetros, con una inferencia de 0.222 ms/imagen. 

**Decisión técnica:** Aunque la CNN logra una arquitectura más compacta en número de parámetros, el modelo denso baseline demostró ser sustancialmente más eficiente en tiempo de cómputo y rendimiento global ($F1 = 0.86$ vs $0.79$) para este escenario específico de 8 épocas en CPU. Por consiguiente, bajo restricciones de recursos, el baseline representa una solución más sostenible y competitiva para este benchmark didáctico.

---

## 5. Model Card, Pruebas, README y Control de Versiones
El proyecto cuenta con un Model Card formal (`MODEL_CARD.md`) que especifica restricciones de uso estrictamente académico y didáctico en Fashion-MNIST, excluyendo entornos de producción críticos o médicos. La suite de pruebas automatizadas con `pytest` (`tests/test_data.py` y `tests/test_model_contract.py`) valida correctamente la normalización de formas y rangos $[0, 1]$ así como el contrato de salida de la CNN (dimensiones $(2, 10)$ y sumatoria de probabilidades softmax igual a 1.0). El código se encuentra estructurado en un repositorio limpio y reproducible bajo control de versiones en Git.