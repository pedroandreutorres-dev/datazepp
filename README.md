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

## ⚙️ Configuración

1. Copia el archivo de ejemplo: `cp .env.example .env`
2. Edita el archivo `.env` y define tu zona horaria en la variable `USER_TIMEZONE`.
   * **¿Cuál es mi zona horaria?**: Debes usar el formato *IANA*. Puedes encontrar el nombre de tu ciudad en esta [Lista de Wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (columna *TZ database name*).
   * **Ejemplos comunes**: 
     * España Peninsular: `Europe/Madrid`
     * Canarias: `Atlantic/Canary`
     * México DF: `America/Mexico_City`
     * Argentina: `America/Argentina/Buenos_Aires`