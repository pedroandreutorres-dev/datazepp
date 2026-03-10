# DataZepp: Biometric Analysis Pipeline

## 1. Objetivo del Proyecto
El propósito de este proyecto es realizar un **Análisis Exploratorio de Datos (EDA)** y un **modelado de composición corporal** a partir de los datos históricos exportados (vía GDPR) de la aplicación **Zepp Life** (Xiaomi Mi Scale).

Se busca transformar datos crudos y semi-estructurados en métricas de salud accionables y tendencias temporales precisas.

---

## 2. Metodología (Roadmap)
El proyecto se desarrollará siguiendo un flujo de trabajo de Ciencia de Datos dividido en cuatro fases:

* **Ingesta**: Carga de archivos JSON/CSV procedentes de la exportación oficial de Zepp en la capa `data/raw`.
* **Procesamiento (ETL)**: Limpieza de ruido, manejo de valores atípicos (*outliers*) y normalización de registros de bioimpedancia.
* **Modelado**: Implementación de ecuaciones de composición corporal para validar y enriquecer las métricas del fabricante.
* **Visualización**: Generación de un dashboard de evolución física y preparación de datos para futuras integraciones (Garmin).

---

## 3. Stack Tecnológico Inicial
* **Lenguaje**: Python 3.10+
* **Análisis de Datos**: `pandas`, `numpy`
* **Visualización**: `matplotlib`, `seaborn`
* **Entorno**: Jupyter Notebooks para experimentación.