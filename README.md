# Grupo-6-Proyecto-VIII-Aprendizaje-No-supervisado

# Clasificación y Clustering de Hongos — Mushroom Dataset

# Índice

1. [Descripción del Dataset](#-descripción-del-dataset)
2. [Exploración y Limpieza de Datos](#-exploración-y-limpieza-de-datos)
    - 2.1. [Análisis Inicial](#-análisis-inicial)
    - 2.2. [Valores Únicos y Variables Constantes](#-valores-únicos-y-variables-constantes)
    - 2.3. [Asociación entre Variables](#-asociación-entre-variables)
3. [Preprocesamiento](#-preprocesamiento)
    - 3.1. [Codificación](#-codificación)
    - 3.2. [Separación de Datos](#-separación-de-datos)
4. [Reducción de Dimensionalidad (PCA)](#-reducción-de-dimensionalidad-pca)
5. [Modelado](#-modelado)
    - 5.1. [Clasificación Supervisada (Random Forest)](#-clasificación-supervisada-random-forest)
    - 5.2. [Clustering No Supervisado (KMeans)](#-clustering-no-supervisado-kmeans)
6. [Visualizaciones](#-visualizaciones)
7. [Conclusiones](#-conclusiones)
8. [Recomendaciones y Próximos Pasos](#-recomendaciones-y-próximos-pasos)
9. [Equipo](#-equipo)
10. [Referencias](#-referencias)
11. [Estructura del Repositorio](#-estructura-del-repositorio)
12. [Contacto](#-contacto)

---


## Descripción del Proyecto

Este proyecto tiene como objetivo analizar y modelar el **Mushroom Dataset** para ayudar a la empresa Délicieux a identificar de manera automática si un hongo es comestible o venenoso, utilizando técnicas de aprendizaje supervisado y no supervisado. El análisis incluye desde la exploración y limpieza de datos hasta la aplicación de modelos de clasificación y clustering, así como la reducción de dimensionalidad mediante PCA.

---

## 1. Descripción del Dataset

- **Fuente:** [Mushroom Dataset - UCI](https://archive.ics.uci.edu/ml/datasets/Mushroom)
- **Instancias:** 8124 hongos
- **Variables:** 23 columnas, todas categóricas
- **Variable objetivo:** `class`  
  - `e`: comestible (edible)
  - `p`: venenoso (poisonous)

Cada fila representa un hongo con atributos como forma, color, olor, características de las láminas, tallo, anillo, hábitat, etc.

---

## 2. Exploración y Limpieza de Datos

### 2.1. Análisis Inicial

- **No hay valores nulos explícitos**, pero la columna `stalk-root` contiene 2480 valores `'?'` que representan datos faltantes.
- **Solución:** Se imputaron estos valores con la moda de la columna para no perder información.

### 2.2. Valores Únicos y Variables Constantes

- Se revisó el número de valores únicos por columna.
- Se eliminó la columna `veil-type` por ser constante (no aporta información).

### 2.3. Asociación entre Variables

- Se utilizó el coeficiente **Cramér's V** para medir la asociación entre variables categóricas.
- Se identificaron variables altamente correlacionadas, lo que ayuda a reducir la dimensionalidad y evitar multicolinealidad.

---

## 3. Preprocesamiento

### 3.1. Codificación

- Todas las variables categóricas se codificaron mediante **One-Hot Encoding**.
- El número de columnas pasó de 22 a 115 tras la codificación.

### 3.2. Separación de Datos

- Se separó la variable objetivo (`class`) del resto de variables predictoras.
- Se realizó un **train-test split** (67% entrenamiento, 33% test).

---

## 4. Reducción de Dimensionalidad (PCA)

- Se aplicó **PCA** para reducir la dimensionalidad y facilitar la visualización.
- Se comprobó que con ~10 componentes principales se retiene la mayor parte de la información y el modelo mantiene un alto rendimiento.

---

## 5. Modelado

### 5.1. Clasificación Supervisada (Random Forest)

- Se entrenó un modelo **Random Forest**.
- **Resultados:**
  - **Accuracy en test:** 1.0000
  - **Precision, Recall, F1-score:** 1.0000
  - **No hay overfitting:** accuracy en train y test idénticos.

### 5.2. Clustering No Supervisado (KMeans)

- Se aplicó **KMeans** tras reducción de dimensionalidad con PCA.
- Se determinó el número óptimo de clusters mediante el método del codo (k=2).
- **Resultados:**
  - **Accuracy (comparando clusters vs clase real):** 0.892
  - **Precision:** 0.982
  - **Recall:** 0.792
  - **F1-score:** 0.876
  - **Homogeneity:** 0.554
  - **Completeness:** 0.574
  - **V-Measure:** 0.564
  - **ARI:** 0.616
  - **FMI:** 0.813

---

## 6. Visualizaciones

- **Heatmap de Cramér's V:** para ver asociaciones entre variables.
- **PCA Scatterplot:** visualización de los datos en 2D coloreados por clase y por cluster.
- **Método del codo:** para determinar el número óptimo de clusters.
- **Catplot:** distribución de la clase real en cada cluster.
- **Matriz de confusión:** comparación entre clusters y clases reales.
- **Gráficos comparativos de métricas:** Random Forest vs KMeans.

---

## 7. Conclusiones

- **Random Forest** logra una clasificación perfecta gracias a la riqueza del dataset y la naturaleza binaria de la variable objetivo.
- **KMeans**, sin usar etiquetas, logra una separación bastante buena, lo que indica que los grupos naturales del dataset coinciden en gran medida con las clases reales.
- Las métricas de clustering permiten evaluar la calidad de los clusters incluso sin etiquetas.
- El análisis exploratorio y la reducción de dimensionalidad son clave para entender y modelar datasets categóricos complejos.

---

## 8. Recomendaciones y Próximos Pasos

- Se recomienda implementar una **plataforma móvil** que permita a los usuarios clasificar hongos en tiempo real, utilizando los modelos desarrollados.
- El pipeline de preprocesamiento y modelado está listo para ser integrado en una API o aplicación móvil.
- Se sugiere seguir monitorizando el modelo con nuevos datos para mantener la precisión y robustez.

---

## 9. Equipo

**ShroomBuster Team**  
A disposición de Délicieux para la siguiente fase del proyecto.

---

## 10. Referencias

- [Mushroom Dataset - UCI](https://archive.ics.uci.edu/ml/datasets/Mushroom)
- [Scikit-learn documentation](https://scikit-learn.org/)
- [Cramér's V — Wikipedia](https://en.wikipedia.org/wiki/Cram%C3%A9r%27s_V)

---

## 11. Estructura del Repositorio

```
├── Data/EDA
│   └── ShroomBuster_Clustering_pca.ipynb
├── docs
│   └── Informe técnico para la empresa Délicieux.pdf
│── .gitignore
├── README.md
└── requirements.txt
```

---

## 12. Contacto

Para cualquier consulta o para avanzar con la integración del modelo en una plataforma móvil, no dudes en contactarnos.

---

**¡Gracias por confiar en nuestro equipo!**

---

**Nota:**  
Este README resume todo el flujo de trabajo, resultados y recomendaciones para el proyecto de clasificación y clustering de hongos. Para detalles técnicos y visualizaciones, consulte el informe técnico adjunto y los notebooks en la carpeta correspondiente.

