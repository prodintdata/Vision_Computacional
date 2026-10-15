# INF-8239 · Unidad 02 · Proyecto de Visión Computacional: Clasificador Visual con CNN y Model Card

**Asignatura:** INF-8239 Ciencia de Datos II  
**Estudiante:** Jhonatan Leandro Cabral Pujols  
**Autor Académico / Base:** Edwin Ramón José Nolasco  
**Código de Entrega:** U02.E04  

Proyecto reproducible para el procesamiento de imágenes, visión computacional, entrenamiento comparativo de arquitecturas neuronales (Baseline Denso vs. CNN), auditoría de costos bajo Green AI y generación de Model Card basado en el dataset *Fashion-MNIST*.

---

## 1. Descripción del Proyecto

Este repositorio integra de forma reproducible las evidencias producidas en el laboratorio LAB07. Su objetivo principal es construir, entrenar y evaluar modelos de clasificación visual supervisada para predecir categorías de prendas de vestir a partir de imágenes de baja resolución ($28 \times 28$ píxeles), manteniendo estrictos controles de reproducibilidad mediante semillas deterministas y asegurando la gestión de dependencias moderna con `uv`.

---

## 2. Estructura del Repositorio

```text
├── data/                      # Directorio de datos (descarga y almacenamiento local)
├── models/                    # Artefactos y pesos serializados (best_cnn.keras, config.json)
├── reports/                   # Métricas, análisis de errores, matrices y visualizaciones
│   ├── cnn_errors.png         # Panel visual de errores de clasificación de la CNN
│   ├── confusion_cnn.png      # Matriz de confusión detallada por clase
│   └── cv_metrics.json        # Consolidado de métricas, parámetros y tiempos
├── scripts/                   # Scripts ejecutables y de auditoría
│   ├── check_runtime.py       # Verificación del entorno, Python, TensorFlow y GPU
│   └── train_cv.py            # Pipeline completo de entrenamiento, evaluación y artefactos
├── src/
│   └── inf8239_u02_cv/
│       ├── __init__.py        # Versión del paquete (0.1.0)
│       ├── data.py            # Funciones de normalización de píxeles y validación estricta
│       └── models.py          # Definición de arquitecturas secuenciales (Dense y CNN)
├── tests/                     # Suite de pruebas unitarias automatizadas
│   ├── test_data.py           # Pruebas de rangos, formas y contratos de datos
│   └── test_model_contract.py # Pruebas de contrato y salida softmax de la CNN
├── pyproject.toml             # Configuración del proyecto, dependencias y extras (CPU/GPU)
├── uv.lock                    # Bloqueo de versiones para reproducibilidad exacta
└── README.md                  # Documentación oficial del proyecto
```

---

## 3. Requisitos Previos

Asegúrese de tener instalado [uv](https://github.com/astral-sh/uv) y Python 3.12 en su estación de trabajo o entorno de desarrollo (como GitHub Codespaces). Sitúese en la raíz del proyecto para ejecutar los siguientes comandos.

1. **Sincronizar el entorno y dependencias:**
   ```bash
   uv sync
   ```

---

## 4. Guía Paso a Paso para Reproducir Resultados

Siga rigurosamente esta secuencia de comandos para verificar el entorno, ejecutar pruebas, entrenar los modelos y generar los reportes analíticos:

### Paso 1: Verificación del Entorno de Ejecución
Compruebe la versión de Python, el sistema operativo, la versión de TensorFlow y la disponibilidad de dispositivos acelerados por GPU:
```bash
uv run python scripts/check_runtime.py
```

### Paso 2: Ejecución de Pruebas Unitarias
Valide que las funciones de procesamiento de datos y los contratos de salida de la red neuronal pasen exitosamente mediante `pytest`:
```bash
uv run pytest -v
```

### Paso 3: Pipeline de Entrenamiento y Evaluación
Ejecute el script de entrenamiento para procesar el dataset Fashion-MNIST, aplicar particiones reproducibles con semilla fija (`SEED = 42`), entrenar ambos modelos (Baseline Denso y CNN) bajo restricciones de épocas, y exportar automáticamente los artefactos en la carpeta `reports/`:
```bash
uv run python scripts/train_cv.py --epochs 8
```
*(Nota: El script genera y actualiza dinámicamente `cv_metrics.json`, `confusion_cnn.png`, `cnn_errors.png` y los pesos óptimos en `models/best_cnn.keras`).*

---

## 5. Interpretación y Uso Responsable

* **Evaluación:** Toda conclusión generada en la carpeta `reports/` separa observación empírica, evidencia cuantitativa de rendimiento ($F1\text{-macro}$), costos computacionales bajo principios de **Green AI** y decisiones arquitectónicas.
* **Limitaciones y Ética:** Este modelo y corpus tienen un propósito **estrictamente académico y didáctico** sobre imágenes de baja resolución ($28 \times 28$). Su uso está **estrictamente prohibido** en entornos de producción críticos, diagnósticos médicos por imagen (OCR avanzado o patología), control de calidad industrial automatizado de alta exigencia o sistemas de vigilancia y seguridad sin un rediseño profundo, validación rigurosa y supervisión humana estricta.
