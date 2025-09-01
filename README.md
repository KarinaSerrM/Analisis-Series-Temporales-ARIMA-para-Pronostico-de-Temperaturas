# Análisis de Series Temporales con Modelos ARIMA para Pronóstico de Temperaturas

Este proyecto documenta el desarrollo de modelos ARIMA (AutoRegressive Integrated Moving Average) para el análisis y pronóstico de temperaturas promedio anuales en Nueva York utilizando datos históricos de 151 años (1870-2020). A través del uso de Python y librerías especializadas como statsmodels, pandas y matplotlib, se implementa un enfoque metodológico dual que combina optimización automática por AIC con interpretación estadística mediante análisis ACF/PACF, priorizando la coherencia teórica sobre la minimización superficial del error.

## Objetivo

Desarrollar un modelo de series temporales robusto que capture patrones climáticos y genere pronósticos realistas, validando estadísticamente la estacionariedad y comparando criterios de selección para determinar la configuración ARIMA óptima que refleje la dinámica real de los datos.

## Flujo de trabajo

### 1. Preparación de datos
- Carga y limpieza del dataset de temperaturas con `pandas`
- Configuración de índice temporal y eliminación de columnas innecesarias
- División estratégica en entrenamiento (90%) y prueba (10%)
- Visualización inicial para identificación de tendencias

### 2. Análisis de estacionariedad
- Implementación de prueba Dickey-Fuller Aumentada (ADF):
  - Verificación automática con valor p
  - Aplicación iterativa de diferenciaciones
  - Confirmación visual de estacionariedad
- Determinación del parámetro d = 1

### 3. Identificación de parámetros
- Generación de gráficos de autocorrelación:
  - ACF (AutoCorrelation Function)
  - PACF (Partial AutoCorrelation Function)
- Búsqueda sistemática de parámetros p y q:
  - Evaluación de 8 configuraciones ARIMA
  - Optimización por Criterio de Información de Akaike (AIC)

### 4. Entrenamiento y predicción
- Ajuste de modelo óptimo: ARIMA(0,1,1) con AIC = 433.66
- Generación de pronósticos con intervalos de confianza al 95%
- Evaluación crítica de predicciones constantes vs. dinámicas

### 5. Validación estadística y comparación
- Métricas de evaluación:
  - RMSE (Root Mean Square Error)
  - MAPE (Mean Absolute Percentage Error)
- Análisis comparativo entre modelos:
  - ARIMA(0,1,1): Menor AIC, predicciones planas
  - ARIMA(1,1,0): Mayor coherencia con ACF/PACF, predicciones dinámicas
- Selección basada en criterio híbrido estadístico-visual

### 6. Análisis crítico y selección final
- Rechazo del modelo con menor AIC por falta de realismo
- Adopción de ARIMA(1,1,0) por coherencia teórica
- Validación de decisión mediante análisis de residuos y tendencias

## Herramientas utilizadas

- Python 3.x
- pandas, NumPy
- matplotlib
- statsmodels
- scipy
- Jupyter Notebook

## Resultados principales

| Métrica | ARIMA(0,1,1) | ARIMA(1,1,0) |
|---------|-------------|-------------|
| AIC | 433.66 | 462.30 |
| RMSE | 1.32°F | 2.11°F |
| MAPE | 1.99% | 3.34% |
| Tipo de predicción | Constante/Plana | Dinámica/Realista |

**Modelo seleccionado**: ARIMA(1,1,0) - Mayor interpretabilidad y coherencia con la estructura de datos

## Conclusiones

- La prueba ADF confirmó la necesidad de una diferenciación (d=1) para lograr estacionariedad
- El análisis ACF/PACF reveló estructura autorregresiva de orden 1, validando la selección de ARIMA(1,1,0)
- La optimización automática por AIC no siempre produce el modelo más interpretable o realista
- El criterio híbrido (métricas + análisis visual + coherencia teórica) genera mejores decisiones de modelado
- Las predicciones dinámicas del modelo final reflejan apropiadamente las tendencias de calentamiento global
