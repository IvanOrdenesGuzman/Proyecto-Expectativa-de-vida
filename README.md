# Analisis de Expectativa de Vida: Escolaridad e Indice de Desarrollo Humano

Proyecto de analisis estadistico desarrollado en Python sobre el dataset **Life Expectancy (WHO)**, que reune informacion de 193 paises entre los anios 2000 y 2015. El trabajo se organiza en tres laboratorios consecutivos, avanzando desde la exploracion de datos hasta la inferencia estadistica formal, en torno a una misma pregunta de investigacion:

> **¿En los paises con un IDH mayor al promedio, cuanto afectan los anios de escolaridad a su expectativa de vida?**

## Resultados principales

- Las variables mas correlacionadas con la expectativa de vida son el Indice de Desarrollo Humano (r = 0.72) y los anios de escolaridad (r = 0.75).
- Para paises con IDH sobre el promedio, la correlacion de Pearson entre escolaridad y expectativa de vida es r = 0.61 (positiva, moderada-fuerte), con un test de significancia que rechaza H0 (p practicamente 0).
- La regresion lineal entre ambas variables arroja `esperanza_de_vida = 1.46 * escolaridad + 54.86`, con R² = 0.37 (37% de la variacion explicada solo por escolaridad).
- El intervalo de confianza al 95.4% para la pendiente, obtenido por Bootstrap (10.000 repeticiones), es [1.467, 1.647], consistente con el valor estimado por regresion.
- El test de comparacion de medias entre paises con 12+ y menos de 12 anios de escolaridad promedio rechaza H0 (T0 = 3.46, p = 0.00033), confirmando una diferencia significativa en expectativa de vida entre ambos grupos.
- La simulacion de Monte Carlo muestra que el IDH es robusto ante variaciones en la escolaridad, aunque mas sensible a caidas que a subidas.

## Estructura del repositorio

```
.
├── notebooks/
│   ├── Expectativa_de_vida.ipynb   # Laboratorio 1 - EDA
│   ├── Parte_2.ipynb               # Laboratorio 2 - Simulacion e Inferencia
│   └── Parte_3.ipynb               # Laboratorio 3 - Intervalos y Test de hipotesis
├── data/
│   └── Life_Expectancy_Data.csv
├── img/
│   ├── mapa_calor_correlaciones.png
│   ├── idh_vs_esperanza_vida.png
│   ├── bootstrap_media_idh.png
│   └── residuos_regresion.png
├── requirements.txt
├── LICENSE
└── README.md
```

## Contenido de los laboratorios

### Laboratorio 1 - Analisis Exploratorio de Datos (`notebooks/Expectativa_de_vida.ipynb`)
- Caracterizacion de las 22 variables del dataset (demograficas, de mortalidad, economicas y de inmunizacion).
- Mapa de calor de correlaciones para identificar las variables mas asociadas a la expectativa de vida.
- Calculo de medidas de tendencia central y dispersion sobre las variables de interes (Escolaridad, IDH, IMC, delgadez).
- Limpieza de datos: tratamiento de valores nulos (imputacion por mediana) y correccion de inconsistencias poblacionales.
- Deteccion y eliminacion de outliers mediante rango intercuartilico (IQR) y diagramas de caja.
- Definicion de la pregunta de investigacion del proyecto.

![Mapa de calor de correlaciones](img/mapa_calor_correlaciones.png)
![IDH vs Esperanza de vida](img/idh_vs_esperanza_vida.png)

### Laboratorio 2 - Simulacion e Inferencia (`notebooks/Parte_2.ipynb`)
- Estimacion puntual del IDH a partir de sus tres componentes (salud, educacion e ingresos).
- Remuestreo **Bootstrap** (10.000 repeticiones) para estimar la distribucion de la media del IDH y de la pendiente entre escolaridad y expectativa de vida.
- **Simulacion de Monte Carlo** para evaluar la sensibilidad del IDH ante variaciones en los anios de escolaridad, modelando la variable mediante una distribucion Beta ajustada a los datos reales.
- Comparacion entre resultados de estimacion puntual y remuestreo.

![Distribucion Bootstrap de la media del IDH](img/bootstrap_media_idh.png)

### Laboratorio 3 - Intervalos de Confianza y Test de Hipotesis (`notebooks/Parte_3.ipynb`)
- Calculo de intervalos de confianza (95.4%) para la media del IDH y para la pendiente escolaridad-expectativa de vida, via Bootstrap.
- Analisis del tamanio muestral y nivel de significancia necesarios para reducir la incertidumbre en un 55%.
- Prueba de bondad de ajuste (Anderson-Darling).
- **Test de hipotesis 1:** comparacion de medias de expectativa de vida entre paises con 12+ y menos de 12 anios de escolaridad promedio (varianza desconocida y heterocedasticidad).
- **Test de hipotesis 2:** significancia del coeficiente de correlacion de Pearson entre escolaridad y expectativa de vida.
- Regresion lineal (calculo manual de pendiente, intercepto, R² y p-value) y analisis de residuos.
- Bonus: replica de la regresion con **scikit-learn** y clasificacion de paises (Desarrollado / En desarrollo) mediante regresion logistica.

![Residuos vs valores ajustados](img/residuos_regresion.png)

## Dataset

`data/Life_Expectancy_Data.csv` - Life Expectancy (WHO), 2938 registros y 22 columnas, con datos de 193 paises entre 2000 y 2015 (fuente original: Organizacion Mundial de la Salud y Naciones Unidas).

## Tecnologias utilizadas

- **Python 3**
- `pandas`, `numpy` - manejo y limpieza de datos
- `matplotlib`, `seaborn` - visualizacion
- `scipy.stats` - pruebas estadisticas e inferencia
- `scikit-learn` - regresion lineal y clasificacion (regresion logistica)

## Como ejecutar

1. Clonar el repositorio:
   ```
   git clone https://github.com/ivanordenes/analisis-datos.git
   cd analisis-datos
   ```
2. Instalar dependencias:
   ```
   pip install -r requirements.txt
   ```
3. Abrir los notebooks en Jupyter o Google Colab y ejecutar las celdas en orden (cada notebook carga el dataset directamente desde su URL en GitHub).

## Limitaciones y proximos pasos

- El modelo de regresion usa una unica variable explicativa (escolaridad); la expectativa de vida es multicausal, por lo que un modelo multivariado podria mejorar el ajuste (R² actual: 0.37).
- La relacion escolaridad-IDH se trata como aproximadamente independiente por simplicidad, aunque en la practica ambas variables se afectan mutuamente en el tiempo.

## Licencia

Este proyecto esta bajo la licencia MIT. Ver el archivo [LICENSE](LICENSE) para mas detalles.

## Autor

Ivan Ordenes - Proyecto realizado como parte del curso de Analisis de Datos / Estadistica.
