# Predicción de fuel_efficiency_mpg (Notebook: regresion_mpg_colab_style.ipynb)

Descripción
-----------
Este notebook (estilo Colab) realiza un flujo completo de regresión supervisada para predecir la eficiencia de combustible (fuel_efficiency_mpg) de vehículos a partir de cuatro variables:
- engine_displacement
- horsepower
- vehicle_weight
- model_year

Se realiza limpieza básica, imputación de valores faltantes, escalado, entrenamiento de modelos lineales y Ridge con búsqueda por rejilla (GridSearchCV), evaluación y visualización de resultados.

Enlace al notebook
------------------
- Notebook (Colab-ready): https://colab.research.google.com/github/jhonnygf/Regresion/blob/main/regresion_mpg_colab_style.ipynb
- En el repo: https://github.com/jhonnygf/Regresion/blob/c8c98f1ad93c141da844544df4567698db17f25d/regresion_mpg_colab_style.ipynb

Dataset
-------
Los datos se cargan desde:
https://raw.githubusercontent.com/bigdatadatafan/datasets-clase/main/car_fuel_efficiency.csv

Columnas usadas:
- engine_displacement
- horsepower (contiene valores NaN)
- vehicle_weight
- model_year
- fuel_efficiency_mpg (target)

Resumen del flujo del notebook
------------------------------
1. Carga y selección de columnas.
2. Revisión de valores faltantes (horsepower tiene NaNs).
3. Imputación (SimpleImputer con estrategia 'median') y escalado (StandardScaler) dentro de pipelines para evitar fugas.
4. Baseline con LinearRegression.
5. Búsqueda de hiperparámetro para Ridge mediante GridSearchCV (α ∈ {0.01, 1, 10, 100}) con KFold(5).
6. Evaluación en el conjunto de test.
7. Visualización (real vs predicho) y presentación de coeficientes estandarizados.

Resultados (ejecutados en el notebook)
--------------------------------------
- Mediana de horsepower (valor usado para la imputación): 149.0
- Baseline LinearRegression -> RMSE ≈ 0.470 | R² ≈ 0.966
- Ridge (GridSearchCV) mejor α = 1
  - RMSE medio (CV) ≈ 0.461 (std ≈ 0.010)
  - RMSE (test) ≈ 0.470 | R² (test) ≈ 0.966

Interpretación rápida de coeficientes (estandarizados)
- vehicle_weight: coeficiente negativo grande → mayor peso reduce mpg.
- horsepower: coeficiente positivo moderado.
- engine_displacement y model_year: efectos muy pequeños comparados con las anteriores.

Reproducción y uso
------------------
1. Abrir el notebook en Colab usando el enlace arriba y seleccionar "Abrir en Colab".
2. Ejecutar las celdas en orden (`Runtime -> Run all`).
3. Si se ejecuta localmente:
   - Instalar dependencias:
     pip install numpy pandas scikit-learn matplotlib
   - Abrir el notebook con Jupyter / JupyterLab y ejecutar las celdas.

Qué puedes cambiar / experimentar
---------------------------------
- Probar otras estrategias de imputación (mean, KNNImputer).
- Añadir polinomios o interacciones si sospechas relaciones no lineales.
- Probar modelos más complejos: RandomForestRegressor, GradientBoosting, XGBoost.
- Evaluar con otros scoring metrics (MAE, adjusted R²).
- Ajustar la rejilla de hiperparámetros para Ridge o explorar Lasso/ElasticNet.

Notas importantes
-----------------
- El pipeline incluye imputación y escalado dentro del flujo para evitar fugas de datos entre train y test.
- horsepower tiene 708 valores NaN (relevante para la imputación).
- Las métricas arriba son las obtenidas en la ejecución guardada en el notebook; debido a la aleatoriedad (aunque se fija RANDOM_STATE=42) pueden variar ligeramente si cambias particionamiento o parámetros.

Estructura del repo
-------------------
- regresion_mpg_colab_style.ipynb — Notebook principal (Colab-ready)

Contacto y contribuciones
-------------------------
- Autor / Mantenimiento: @jhonnygf
- Para sugerencias o PRs: abrir issue o pull request en el repositorio.


Gracias
