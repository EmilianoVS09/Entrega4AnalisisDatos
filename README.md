# Evento Evaluativo 4 - Análisis de Datos

**Asignatura:** Análisis de Datos
**Carrera:** Ingeniería de Sistemas / Ciencia de Datos
**Periodo:** 2025-2
**Equipo:** 7
**Docente:** Daniel Alexis Nieto Mora

## Integrantes del equipo

| # | Nombre |
|---|---|
| 1 | Carlos Alberto Moreno David |
| 2 | Juan Esteban García Ocampo |
| 3 | Emiliano Vélez Suárez |
| 4 | Sebastián Ciro Medellín |

---

## Descripción general

Este repositorio contiene la entrega del Evento Evaluativo 4 de la asignatura
Análisis de Datos. El objetivo del evento es aplicar técnicas de **Machine Learning
supervisado y no supervisado** sobre datasets reales y justificar las decisiones
técnicas con base en el análisis exploratorio, la selección de algoritmos, las
métricas y la interpretación de los resultados.

Al equipo 7 le correspondieron los **Ejercicios 2 y 4** del enunciado.

### Ejercicio 2 - Clasificación de tumores malignos y benignos
- **Dataset:** Breast Cancer Wisconsin (Diagnostic) - 569 muestras, 30 variables.
- **Tipo de problema:** Clasificación binaria supervisada (M = Maligno, B = Benigno).
- **Algoritmos aplicados:** Regresión Logística, SVM (kernel RBF) y Random Forest.
- **Métricas:** Accuracy, F1-Score, Precision, Recall y Matriz de Confusión.
- **Visualización:** PCA 2D con elipses de confianza para evidenciar la
  separabilidad entre clases.

### Ejercicio 4 - Agrupamiento de clientes según comportamiento de compra
- **Dataset:** Mall Customers - 200 clientes con variables demográficas y de consumo.
- **Tipo de problema:** Clustering no supervisado.
- **Algoritmos aplicados:** K-Means, DBSCAN y Clustering Jerárquico (enlace Ward).
- **Métricas:** Silhouette Score, método del codo, búsqueda de hiperparámetros y
  visualización PCA 2D/3D.
- **Salida:** Interpretación de los 5 segmentos de mercado identificados y propuesta
  de estrategia comercial para cada uno.

---

## Estructura del repositorio

```
Entrega4AnalisisDatos/
├── Data/
│   ├── Breast_Cancer.csv          # Dataset del Ejercicio 2 (569 x 33)
│   └── Mall_Customers.csv         # Dataset del Ejercicio 4 (200 x 5)
├── Notebooks/
│   ├── Ejercicio_2_Breast_Cancer.ipynb
│   └── Ejercicio_4_Mall_Customers.ipynb
├── Exposicion/
│   └── Exposicion_Evento4.html    # Presentación interactiva (slides + métricas)
├── README.md
└── .gitignore
```

---

## Cómo ejecutar los notebooks

### Requisitos
- Python >= 3.10
- Librerías: `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`, `scipy`,
  `jupyter`.

Instalación rápida:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy jupyter
```

### Ejecución

```bash
cd Notebooks
jupyter notebook Ejercicio_2_Breast_Cancer.ipynb
jupyter notebook Ejercicio_4_Mall_Customers.ipynb
```

Las rutas a los datasets dentro de cada notebook son **relativas** a la carpeta
`Notebooks/` (`../Data/...`), por lo que conviene abrirlos desde esa carpeta.

### Exposición

El archivo `Exposicion/Exposicion_Evento4.html` se abre directamente en cualquier
navegador moderno (no requiere servidor). Está autocontenido: las gráficas están
embebidas como imágenes en base64.

---

## Resumen de resultados

### Ejercicio 2 - Métricas en conjunto de prueba (n = 114)

| Modelo | Accuracy | Precision (M) | Recall (M) | F1 (M) | FP | FN |
|---|---|---|---|---|---|---|
| Regresión Logística | 0.9649 | 0.975 | 0.929 | 0.9512 | 1 | 3 |
| SVM (RBF) | **0.9737** | **1.000** | 0.929 | **0.9630** | 0 | 3 |
| Random Forest | **0.9737** | **1.000** | 0.929 | **0.9630** | 0 | 3 |

PCA explica el **63.2 %** de la varianza con solo 2 componentes y muestra
separabilidad clara entre clases.

### Ejercicio 4 - Calidad de los clusters

| Algoritmo | Silhouette Score | Nº Clusters |
|---|---|---|
| K-Means (k=5, 2D) | **0.5547** | 5 |
| Jerárquico Ward (k=5, 2D) | 0.5538 | 5 |
| DBSCAN (eps=0.35, ms=3) | 0.4756 | 7 + 11 ruido |
| K-Means (k=8, 4D) | 0.3874 | 8 |

Los **5 segmentos** identificados con K-Means en el espacio
`Income x SpendingScore` son: VIP, Promedio, Conservadores Pudientes,
Impulsivos Maduros y Precavidos Jóvenes.

---

## Decisiones técnicas destacadas

- **Estandarización (`StandardScaler`)** antes de cualquier modelo basado en
  distancias o coeficientes, para neutralizar la diferencia de escalas entre
  variables.
- **Partición estratificada (80/20)** en el Ejercicio 2, para preservar la
  proporción de tumores malignos en train y test.
- **Validación cruzada 5-fold estratificada** sobre F1 para confirmar la
  estabilidad de los modelos del Ejercicio 2.
- **Selección de k** en el Ejercicio 4 mediante la combinación del método del
  codo y el pico del Silhouette Score (ambos coinciden en k=5).
- **Búsqueda de hiperparámetros para DBSCAN** sobre una rejilla de `eps`
  (0.30 a 1.50) y `min_samples` (3, 5, 7, 10), optimizando el Silhouette Score.
- **PCA 2D y 3D** para reducir el espacio de features y visualizar la
  separabilidad de las clases y la coherencia de los clusters.

---

## Reproducibilidad

- `random_state = 42` en todos los algoritmos con componente aleatoria.
- `n_init = 50` en K-Means para mitigar la dependencia de la inicialización.
- Los notebooks fueron re-ejecutados completos desde un kernel limpio antes
  de la entrega y no contienen celdas con errores.
