# DataZepp: Biometric Analysis Pipeline

## 1. Objetivo del Proyecto
El propósito de este proyecto es transformar los datos históricos de composición corporal exportados de la aplicación **Zepp Life** (Xiaomi Mi Scale) en un sistema de seguimiento biométrico profesional. 

El sistema automatiza la limpieza de registros, gestiona husos horarios de forma precisa y mantiene un histórico incremental diseñado para el análisis estadístico y la exportación de datos a ecosistemas de terceros.

---

## 2. Arquitectura de Datos (Pipeline)
El proyecto sigue un flujo de trabajo de **Ingeniería de Datos** dividido en capas para asegurar la integridad y trazabilidad de la información:

* **Capa Raw (Bronce)**: Ingesta de archivos CSV con nombres dinámicos procedentes de la exportación de Zepp. El sistema detecta el archivo automáticamente, procesa los datos y elimina el origen para mantener la carpeta limpia.
* **Procesamiento (ETL - Plata)**: 
    * **Limpieza**: Filtrado de registros incompletos (eliminación de filas sin datos de bioimpedancia).
    * **Normalización**: Redondeo técnico de métricas y formateo de tipos de datos.
    * **Gestión Temporal**: Conversión de UTC a hora local mediante variables de entorno y *Feature Engineering* (extracción de hora, día de la semana e indicadores de fin de semana).
* **Capa Maestra (Oro)**: Almacenamiento incremental en `body_composition_master.csv`. El sistema utiliza una lógica de **Carga Delta** que evita duplicados comparando las marcas de tiempo exactas.
* **Capa de Salida (Buffer)**: Generación de `garmin_pending.csv`, un archivo que actúa como cola de exportación para nuevos registros pendientes de sincronizar.

---

## 3. Futuras Integraciones: Garmin Connect (FIT)
Una de las metas principales de DataZepp es la sincronización con el ecosistema Garmin. 

**Hoja de ruta**: Se implementará un script específico de conversión para transformar el archivo `garmin_pending.csv` al formato estándar **.FIT** (Flexible and Interoperable Data Transfer). 
* Este script leerá exclusivamente los registros acumulados en la cola de pendientes.
* Una vez generados los archivos FIT y confirmada su exportación, el sistema purgará automáticamente el archivo de pendientes para garantizar que no se suban datos duplicados a Garmin Connect.

---

## 4. Stack Tecnológico
* **Lenguaje**: Python 3.10+
* **Librerías Core**: `pandas` (procesamiento), `python-dotenv` (configuración), `glob` (gestión de archivos).
* **Entorno**: VS Code + Jupyter Notebooks.

---

## ⚙️ Configuración del Entorno

Este proyecto utiliza un archivo de configuración para gestionar la localización de los datos:

1.  **Variables de Entorno**:
    * Copia el archivo de ejemplo: `cp .env.example .env`
    * Edita el archivo `.env` y define tu zona horaria en la variable `USER_TIMEZONE`.
2.  **Identificación de Zona Horaria**:
    * Debes usar el formato *IANA*. Puedes encontrar el identificador de tu ciudad en la [Lista de zonas horarias de Wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (columna *TZ database name*).
    * **Ejemplos**: 
        * España Peninsular: `Europe/Madrid`
        * Canarias: `Atlantic/Canary`
        * Argentina: `America/Argentina/Buenos_Aires`
3.  **Flujo de Trabajo Diario**:
    * Coloca el CSV exportado de Zepp en la carpeta `data/raw/`.
    * Ejecuta el notebook `01_eda_zepp.ipynb`. 
    * El sistema actualizará automáticamente el historial maestro, preparará la cola para Garmin y eliminará el archivo procesado de `data/raw/`.