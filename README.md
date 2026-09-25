# Análisis de Expectativa de Vida: Escolaridad e Índice de Desarrollo Humano

Proyecto de análisis estadístico desarrollado en Python sobre el dataset **Life Expectancy (WHO)**, que reúne información de 193 países entre los años 2000 y 2015. El trabajo se organiza en tres laboratorios consecutivos, avanzando desde la exploración de datos hasta la inferencia estadística formal, en torno a una misma pregunta de investigación:

> **¿En los países con un IDH mayor al promedio, cuánto afectan los años de escolaridad a su expectativa de vida?**

## Estructura del proyecto

### 📊 Laboratorio 1 — Análisis Exploratorio de Datos (`Expectativa_de_vida.ipynb`)
- Caracterización de las 22 variables del dataset (demográficas, de mortalidad, económicas y de inmunización).
- Mapa de calor de correlaciones para identificar las variables más asociadas a la expectativa de vida.
- Cálculo de medidas de tendencia central y dispersión sobre las variables de interés (Escolaridad, IDH, IMC, delgadez).
- Limpieza de datos: tratamiento de valores nulos (imputación por mediana) y corrección de inconsistencias poblacionales.
- Detección y eliminación de outliers mediante rango intercuartílico (IQR) y diagramas de caja.
- Definición de la pregunta de investigación del proyecto.

### 🎲 Laboratorio 2 — Simulación e Inferencia (`Parte_2.ipynb`)
- Estimación puntual del IDH a partir de sus tres componentes (salud, educación e ingresos).
- Remuestreo **Bootstrap** (10.000 repeticiones) para estimar la distribución de la media del IDH y de la pendiente entre escolaridad y expectativa de vida.
- **Simulación de Monte Carlo** para evaluar la sensibilidad del IDH ante variaciones en los años de escolaridad, modelando la variable mediante una distribución Beta ajustada a los datos reales.
- Comparación entre resultados de estimación puntual y remuestreo.

### 📐 Laboratorio 3 — Intervalos de Confianza y Test de Hipótesis (`Parte_3.ipynb`)
- Cálculo de intervalos de confianza (95,4%) para la media del IDH y para la pendiente escolaridad–expectativa de vida, vía Bootstrap.
- Análisis del tamaño muestral y nivel de significancia necesarios para reducir la incertidumbre en un 55%.
- Prueba de bondad de ajuste (Anderson-Darling).
- **Test de hipótesis 1:** comparación de medias de expectativa de vida entre países con ≥12 y <12 años de escolaridad promedio (varianza desconocida y heterocedasticidad).
- **Test de hipótesis 2:** significancia del coeficiente de correlación de Pearson entre escolaridad y expectativa de vida.
- Regresión lineal (cálculo manual de pendiente, intercepto, R² y p-value) y análisis de residuos.
- Bonus: réplica de la regresión con **scikit-learn** y clasificación de países (Desarrollado / En desarrollo) mediante regresión logística.

## Dataset

`Life_Expectancy_Data.csv` — Life Expectancy (WHO), 2938 registros y 22 columnas, con datos de 193 países entre 2000 y 2015 (fuente original: Organización Mundial de la Salud y Naciones Unidas).

## Tecnologías utilizadas

- **Python 3**
- `pandas`, `numpy` — manejo y limpieza de datos
- `matplotlib`, `seaborn` — visualización
- `scipy.stats` — pruebas estadísticas e inferencia
- `scikit-learn` — regresión lineal y clasificación (regresión logística)

## Cómo ejecutar

1. Clonar el repositorio.
2. Instalar dependencias: `pip install pandas numpy matplotlib seaborn scipy scikit-learn`
3. Abrir los notebooks en Jupyter o Google Colab y ejecutar las celdas en orden (cada notebook carga el dataset directamente desde su URL en GitHub).

## Autor

Iván Ordenes — Proyecto realizado como parte del curso de Análisis de Datos / Estadística.
