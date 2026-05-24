# 📊 Proyecto de Análisis de Datos — ConnectaTel

## 📌 Descripción del proyecto

Este proyecto consiste en un análisis exploratorio y limpieza de datos para la empresa ficticia de telecomunicaciones **ConnectaTel** en Latinoamérica.

El objetivo principal es analizar el comportamiento de los usuarios utilizando información histórica registrada hasta el año 2024.

Durante el desarrollo del notebook se realizan tareas de:

- Carga y exploración de datasets
- Evaluación de calidad de datos
- Limpieza y transformación de información
- Identificación de valores nulos y sentinels
- Estandarización de fechas
- Generación de métricas de uso por usuario
- Segmentación de clientes
- Visualización de datos
- Análisis de comportamiento de usuarios

---

# 🗂️ Datasets utilizados

El análisis utiliza tres archivos CSV:

| Archivo | Descripción |
|---|---|
| `plans.csv` | Información de planes telefónicos (precio, GB, minutos incluidos, costos extra) |
| `users.csv` | Información demográfica y de suscripción de usuarios |
| `usage.csv` | Historial de uso de llamadas y mensajes |

---

# 🧰 Tecnologías utilizadas

- Python 3
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn

---

# 📚 Objetivos del análisis

## 1. Exploración inicial

- Cargar datasets
- Revisar estructura y tipos de datos
- Detectar inconsistencias iniciales

## 2. Calidad de datos

- Identificación de valores nulos
- Detección de sentinels
- Validación de fechas
- Revisión de valores inválidos

## 3. Limpieza de datos

- Reemplazo de sentinels
- Corrección de fechas fuera de rango
- Tratamiento de valores nulos
- Conversión de tipos de datos

## 4. Análisis de comportamiento

- Métricas de uso por usuario
- Agrupación de usuarios por nivel de uso
- Segmentación por edad
- Comparación entre planes Premium y Básico

## 5. Visualización

- Distribución de usuarios por edad
- Distribución de usuarios por nivel de uso
- Comparaciones entre grupos
- Estadísticas descriptivas

---

# 🧹 Principales problemas encontrados

Durante el análisis se detectaron distintos problemas de calidad de datos:

- Valores sentinels en la columna `age` (`-999`)
- Valores faltantes en `city`
- Fechas fuera de rango (`2026`)
- Valores nulos estructurales en `duration` y `length`
- Distribuciones sesgadas en algunas variables numéricas

---

# 🧠 Principales decisiones tomadas

## Valores sentinels

Los valores `-999` en la edad fueron reemplazados utilizando la mediana.

## Fechas inválidas

Las fechas posteriores a 2024 fueron marcadas como valores nulos.

## Valores nulos estructurales

Se identificó que algunos valores nulos eran esperados:

- `duration` es nulo cuando el tipo es `text`
- `length` es nulo cuando el tipo es `call`

Por lo tanto, estos nulos fueron conservados.

---

# 👥 Segmentación de usuarios

## Segmentación por edad

Los usuarios fueron clasificados en:

- Joven
- Adulto
- Adulto Mayor

## Segmentación por uso

Los usuarios fueron agrupados según su actividad:

- Bajo uso
- Medio uso
- Alto uso

La clasificación se realizó utilizando métricas agregadas de llamadas y mensajes.

---

# 📈 Resultados generales

Algunos hallazgos relevantes:

- El plan más utilizado es el plan Básico.
- La mayoría de usuarios pertenecen al grupo Adulto.
- Existen diferencias de comportamiento entre grupos etarios.
- El análisis permitió reducir significativamente problemas de calidad de datos.

---

# ▶️ Cómo ejecutar el proyecto

## 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
```

## 2. Instalar dependencias

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

## 3. Ejecutar Jupyter Notebook

```bash
jupyter notebook
```

Abrir el archivo:

```bash
S7 Version-Estudiante-Project-ConnectaTel.ipynb
```

---

# 📂 Estructura sugerida del proyecto

```text
📁 proyecto-connectatel/
│
├── 📄 README.md
├── 📄 S7 Version-Estudiante-Project-ConnectaTel.ipynb
├── 📁 data/
│   ├── plans.csv
│   ├── users.csv
│   └── usage.csv
│
└── 📁 images/
```

---

# 🚀 Posibles mejoras futuras

- Crear modelos predictivos de churn
- Implementar clustering de usuarios
- Automatizar limpieza de datos
- Crear dashboards interactivos
- Analizar consumo mensual por usuario

---

# 👨‍💻 Autor

Proyecto desarrollado como práctica de análisis de datos y limpieza de datasets utilizando Python y Pandas.

---

# 📄 Licencia

Este proyecto tiene fines educativos y académicos.

