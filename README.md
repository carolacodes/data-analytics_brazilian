# Data_Brazilian — Olist (ETL + Modelo Estrella + Postgres)

Proyecto de análisis de datos usando el dataset **Brazilian E-Commerce (Olist)**.  
Incluye: exploración, limpieza, carga a Postgres (staging) y construcción de un **modelo estrella** (analytics) para visualización en BI (ej. Metabase).

---

## Requisitos

- Python 3.13+ (recomendado)
- PostgreSQL + pgAdmin (local)
- VS Code (opcional, recomendado)

---

## Estructura del proyecto

- `data/`  
  Carpeta con los CSV originales descargados de Kaggle (dataset Olist).

- `venv/`  
  Entorno virtual local (NO se sube a GitHub).

- `.env`  
  Variables de entorno para la conexión a Postgres (NO se sube a GitHub).

- `.gitignore`  
  Exclusiones de Git (venv, .env, checkpoints, etc.).

- `requirements.txt`  
  Dependencias para reproducir el entorno.

- `conexion_bd.ipynb`  
  Notebook para **configurar y probar la conexión** a Postgres desde Python.

- `exploracion_olist.ipynb`  
  Notebook para **explorar** los CSV (head/info, nulos, duplicados, tipos, etc.).

- `01_staging_limpieza_olist.ipynb`  
  Notebook para **limpieza + estandarización** de datos y carga a Postgres en el schema **`staging`**.

- `02_modelo_estrella_olist.ipynb`  
  Notebook para construir el **modelo estrella** (schema **`analytics`**): dimensiones y tabla de hechos.

---

## Instalación y ejecución (paso a paso)

### 1) Clonar el repositorio

```bash
git clone <URL_DEL_REPO>
cd DATA_BRAZILIAN
```

# 2) Crear y activar entorno virtual

### Windows (PowerShell)

```bash
python -m venv venv
venv\Scripts\Activate.ps1
```

Si PowerShell bloquea la ejecución de scripts:

```bash
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### Windows (CMD)

```bash
python -m venv venv
venv\Scripts\activate.bat
```

# 3) Instalar dependencias

```bash
pip install -r requirements.txt
```

Si querés regenerar requirements.txt:

```bash
pip freeze > requirements.txt
```

# 4) Configurar variables de entorno (.env)

Crear un archivo .env en la raíz del proyecto con:

```bash
DB_HOST=localhost
DB_PORT=5432
DB_NAME=TU_DB
DB_USER=postgres
DB_PASSWORD=TU_PASSWORD
```

Importante: este archivo no se sube al repo.

# 5) Preparar Postgres (schemas)

En pgAdmin (sobre tu base de datos):

```sql
CREATE SCHEMA IF NOT EXISTS staging;
CREATE SCHEMA IF NOT EXISTS analytics;
```

# 6) Ejecutar notebooks (orden recomendado)

1. conexion_bd.ipynb

2. Verifica conexión a Postgres.

3. Prueba lectura/escritura básica.

4. exploracion_olist.ipynb

5. Analiza CSV: tipos, nulos, duplicados, valores únicos.

01_staging_limpieza_olist.ipynb

5. Limpia y estandariza datasets. Carga tablas en staging.\* (ej: staging.orders_stg, staging.customers_stg, etc.)

02_modelo_estrella_olist.ipynb

- Crea dimensiones (analytics.dim\_\*)

- Crea tabla de hechos (analytics.fact_order_items)

- Deja lista la base para BI.

# Cómo abrir Jupyter

Si no lo tenés instalado:

```bash
pip install jupyter notebook
```

Iniciar:

```bash
jupyter notebook
```

Se abrirá en el navegador. Luego elegí el notebook a ejecutar.

# Notas sobre GitHub

### No se deben subir:

venv/

.env

.ipynb_checkpoints/

archivos grandes (datasets), salvo que el proyecto lo requiera

### Los compañeros deben:

- clonar el repo

- crear venv

- instalar requirements.txt

- crear su .env

- correr notebooks en orden

- Dataset

### Fuente: Kaggle — “Brazilian E-Commerce Public Dataset by Olist”

(CSV dentro de data/)
