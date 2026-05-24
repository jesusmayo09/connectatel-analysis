# ConnectaTel - Análisis de Comportamiento de Clientes

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Python](https://img.shields.io/badge/python-3.7+-blue)
![Datasets](https://img.shields.io/badge/datasets-3-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 Descripción del Proyecto

**ConnectaTel** es un proyecto de análisis de datos para una empresa de telecomunicaciones en Latinoamérica. Como **analista de datos**, el objetivo es evaluar el **comportamiento de los clientes**, identificar **patrones de consumo**, detectar **comportamientos atípicos** y crear **segmentos de clientes** para diseñar estrategias de retención y mejora de planes.

El análisis trabaja con datos registrados **hasta el año 2024**, permitiendo una visión completa del comportamiento del negocio en ese período.

### 🎯 Objetivos Principales

- ✅ Explorar, limpiar y validar tres datasets de telecomunicaciones
- ✅ Construir un **perfil estadístico** de los clientes
- ✅ Detectar **comportamientos atípicos** (outliers)
- ✅ Crear **segmentos de clientes** por edad y nivel de uso
- ✅ Identificar **patrones de consumo** diferenciales
- ✅ Generar **recomendaciones de negocio** para planes y estrategias de retención

---

## 📊 Datasets Utilizados

El proyecto trabaja con **tres datasets** en formato CSV:

### 1️⃣ **plans.csv** - Información de Planes
Contiene los detalles de los planes de telecomunicaciones ofrecidos.

| Campo | Descripción | Tipo |
|-------|-------------|------|
| `plan_name` | Nombre del plan (Basico, Premium) | String |
| `messages_included` | Mensajes incluidos en el plan | Integer |
| `gb_per_month` | GB de datos por mes | Integer |
| `minutes_included` | Minutos incluidos en el plan | Integer |
| `usd_monthly_pay` | Pago mensual en USD | Float |
| `usd_per_gb` | Costo por GB adicional | Float |
| `usd_per_message` | Costo por mensaje adicional | Float |
| `usd_per_minute` | Costo por minuto adicional | Float |

**Ejemplo:**
- **Plan Básico**: $12/mes, 100 mensajes, 5GB, 100 minutos
- **Plan Premium**: $25/mes, 500 mensajes, 20GB, 600 minutos

---

### 2️⃣ **users_latam.csv** - Información de Clientes
Contiene datos demográficos y de suscripción de los clientes.

| Campo | Descripción | Tipo | Notas |
|-------|-------------|------|-------|
| `user_id` | Identificador único del usuario | Integer | PK |
| `first_name` | Nombre del cliente | String | |
| `last_name` | Apellido del cliente | String | |
| `age` | Edad del cliente | Integer | Valores faltantes y sentinels (`?`) |
| `city` | Ciudad de residencia | String | Valores faltantes y sentinels (`?`) |
| `reg_date` | Fecha de registro | DateTime | Algunas fechas > 2024 |
| `plan` | Plan contratado | String | Basico / Premium |
| `churn_date` | Fecha de cancelación (si aplica) | DateTime | NaN si cliente activo |

**Nota de limpieza:** Se detectaron y corrigieron valores faltantes, sentinels (`?`), y fechas fuera de rango.

---

### 3️⃣ **usage.csv** - Detalle de Uso
Contiene el registro del uso real de servicios (llamadas y mensajes).

| Campo | Descripción | Tipo | Notas |
|-------|-------------|------|-------|
| `user_id` | Identificador del usuario | Integer | FK a users |
| `type` | Tipo de servicio | String | "call" o "message" |
| `duration` / `length` | Duración de llamada o mensajes | Integer | **Valores faltantes estructurales** (MAR) |

**Problemas detectados:**
- Valores faltantes **dependientes del tipo de servicio**:
  - Si `type = "call"` → `duration` contiene valor, `length` es NaN
  - Si `type = "message"` → `length` contiene valor, `duration` es NaN

---

## 🧩 Estructura del Análisis (8 Pasos)

El notebook está organizado en **8 pasos progresivos** de análisis:

### **Paso 1: Cargar y Explorar**
- Importar librerías necesarias (pandas, numpy, seaborn, matplotlib)
- Cargar los 3 datasets en memoria
- Visualizar primeras filas y estructura
- Validar carga correcta de archivos

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

plans = pd.read_csv('/datasets/plans.csv')
users = pd.read_csv('/datasets/users_latam.csv')
usage = pd.read_csv('/datasets/usage.csv')
```

---

### **Paso 2: Perfilar Datos**
- Analizar tipos de datos
- Identificar valores faltantes y anomalías
- Detectar duplicados
- Comprender dimensiones y cobertura de datos

**Métricas clave:**
- Total de usuarios
- Distribución por plan
- Rango de edades
- Período de tiempo de datos

---

### **Paso 3: Limpiar Datos**
- **Manejo de valores faltantes:**
  - `age` y `city` con valores sentinels (`?`)
  - `duration` y `length` con MAR estructural
  
- **Validación de fechas:**
  - Eliminar `reg_date` > 2024
  - Validar coherencia `reg_date` < `churn_date`
  
- **Tratamiento de outliers:**
  - Identificar patrones anormales de uso
  - Decidir mantener o remover

---

### **Paso 4: Enriquecer y Transformar**
- Crear **variables derivadas**:
  - `grupo_edad`: Segmentación por rango de edad
    - Joven (0-30 años)
    - Adulto (30-60 años)
    - Adulto Mayor (60+ años)
  
  - `grupo_uso`: Segmentación por nivel de uso
    - Bajo uso
    - Medio uso
    - Alto uso
  
  - `churn_status`: Indicador de cancelación
  - `tempo_vigencia`: Meses activo como cliente

---

### **Paso 5: Analizar Distribuciones**
- Gráficos univariados por variable
- Estadísticas descriptivas (media, mediana, desv. est.)
- Identificar distribuciones sesgadas
- Detectar necesidad de transformaciones

---

### **Paso 6: Analizar Relaciones**
- Relación entre edad y tipo de plan
- Relación entre uso y plan
- Relación entre duración como cliente y churn
- Matriz de correlación

---

### **Paso 7: Segmentación de Clientes**
- **Segmentación por edad:**
  - Distribución de planes por grupo etario
  - Comportamiento de uso por edad
  
- **Segmentación por uso:**
  - Proporción de usuarios en cada nivel
  - Diferencias entre planes
  
- **Identificación de oportunidades:**
  - Usuarios de alto uso en plan Básico (candidatos a upgrade)
  - Grupos desatendidos

---

### **Paso 8: Documentación y Deploy**
- Subir notebook a GitHub
- Crear README completo
- Documentar pasos de reproducción
- Establecer commit history limpio

---

## 🔍 Hallazgos Principales

### ⚠️ Problemas Detectados en los Datos

1. **Valores faltantes en `age` y `city`**
   - Presencia de sentinels (`?`)
   - Requirió limpieza e imputación selectiva

2. **Valores faltantes estructurales en `usage`**
   - `duration` faltante cuando `type = "message"`
   - `length` faltante cuando `type = "call"`
   - Patrón Missing At Random (MAR)

3. **Fechas fuera de rango**
   - Algunas `reg_date` posteriores a 2024
   - Requirió validación y filtrado

---

### 📊 Segmentación por Edad

| Segmento | Tamaño | Plan Básico | Plan Premium |
|----------|--------|------------|-------------|
| **Joven** (0-30) | Menor | 64.1% | 35.9% |
| **Adulto** (30-60) | Mayor | 65.5% | 34.5% |
| **Adulto Mayor** (60+) | Medio | 64.2% | 35.8% |

**Insight:** La adopción de Premium es **uniforme** (~35%) entre todos los segmentos de edad.

---

### 📈 Segmentación por Nivel de Uso

| Nivel de Uso | Básico | Premium | Observación |
|-------------|--------|---------|-------------|
| **Bajo uso** | 70.0% | 70.5% | Mayoría de usuarios |
| **Medio uso** | 28.5% | 28.1% | Usuarios moderados |
| **Alto uso** | 1.5% | 1.5% | Minoría activa |

**Insight:** La cantidad de **mensajes y llamadas no es diferenciador** entre planes. Los usuarios de alto uso están distribuidos equitativamente.

---

### 💡 Recomendaciones de Negocio

#### 1. **Planes Diferenciados por Datos (GB)**
- El factor diferenciador principal es la **cantidad de GB**, no mensajes/minutos
- Considerar planes con énfasis en datos ilimitados
- Revisar pricing de GB adicionales ($1.0-$1.2 es competitivo pero mejorable)

#### 2. **Estrategia de Marketing Agnóstica a Edad**
- No enfocarse en un rango de edad específico
- Todos los grupos tienen adopción similar de Premium
- Estrategia horizontal en lugar de vertical por demográfica

#### 3. **Campaña de Upgrade para Alto Uso**
- Identificar el **1.5% de usuarios de alto uso en plan Básico**
- Ofrecerles descuentos o promociones para migrar a Premium
- Reducirían cargos excedentes y aumentarían ARPU

#### 4. **Revisión de Plan Básico**
- Los 100 minutos y 100 mensajes están **infrautilizados**
- Considerar reducir estos números (ahorro de costos)
- Compensar con mejor pricing en datos

#### 5. **Nuevos Planes Intermedios**
- Considerar plan "Pro" entre Básico y Premium
- Segmentación: 10GB, 300 minutos, $18-$20/mes
- Capturar usuarios de medio uso que podrían escalar

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

