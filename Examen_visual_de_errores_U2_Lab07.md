### 6. Análisis Visual de Errores y Conclusiones (CNN)

Tras examinar detalladamente la matriz de errores (`reports/cnn_errors.png`), donde **R** representa la etiqueta real (*Real*) y **P** la predicción incorrecta del modelo (*Predicted*), se realizó un conteo y categorización de las equivocaciones visuales más frecuentes:

* **Categoría 4 (Abrigos / Coats):** Concentra la mayor cantidad de errores (4 apariciones), siendo confundida principalmente con prendas similares de la categoría 2 (pulóveres).
* **Categorías 3 (Vestidos) y 6 (Camisas):** Siguen en frecuencia con 3 errores cada una.
* **Categoría 9 (Botines / Ankle boots):** Presenta 2 errores de clasificación.
* **Categorías 0 (T-shirt/top), 2 (Pullover), 5 (Sandalias) y 7 (Zapatillas):** Registran 1 error individual cada una.

#### Conclusión principal sobre los errores:
La gran mayoría de las confusiones del modelo se concentran en las **prendas del tren superior y vestidos** (abrigos, camisas, vestidos y pulóveres). 

Esto ocurre porque, a diferencia de categorías como los pantalones (clase 1) o los bolsos (clase 8), que poseen siluetas muy geométricas y aisladas, las prendas superiores comparten una enorme cantidad de características morfológicas y texturas similares en una resolución reducida de $28\times28$ píxeles (como mangas largas, pliegues y líneas de solapa), lo que genera una alta ambigüedad visual que los filtros de la CNN encuentran difícil de separar sin una resolución o profundidad de red mayor.