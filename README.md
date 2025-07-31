# 📊 Análisis de Churn de Clientes - TELECOM X

## 📋 Descripción del Proyecto

Este proyecto analiza la **evasión de clientes (churn)** de la empresa TELECOM X mediante técnicas de análisis de datos. La empresa enfrenta serias dificultades para mantener la confianza de sus clientes, generando cancelaciones masivas en los distintos servicios que ofrece. El objetivo es identificar patrones y factores que influyen en la pérdida de clientes para proponer estrategias de retención efectivas.

## 🎯 Objetivos

- **Objetivo Principal:** Analizar la evasión de clientes de TELECOM X mediante análisis de datos.
- **Objetivos Específicos:**
  - Implementar procesos de ETL (Extracción, Transformación y Carga).
  - Realizar un Análisis Exploratorio de Datos (EDA).
  - Identificar patrones y factores que influyen en el churn.
  - Proponer recomendaciones para reducir la tasa de abandono.

## 📊 Dataset

### Fuente de Datos

- **Origen:** Datos JSON de TELECOM X
- **URL:** [https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/main/TelecomX_Data.json](https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/main/TelecomX_Data.json)
- **Registros:** 7,043 clientes (después de limpieza)
- **Variables:** 21 columnas

### Estructura de Datos

**Información del Cliente**
- `customerID`: ID único del cliente
- `gender`: Género (Masculino/Femenino)
- `SeniorCitizen`: Cliente mayor de 65 años (0/1)
- `Partner`: Tiene pareja (Yes/No)
- `Dependents`: Tiene dependientes (Yes/No)
- `tenure`: Meses de permanencia

**Servicios Telefónicos**
- `PhoneService`: Servicio telefónico (Yes/No)
- `MultipleLines`: Múltiples líneas telefónicas

**Servicios de Internet**
- `InternetService`: Tipo de internet (DSL/Fiber optic/No)
- `OnlineSecurity`: Seguridad online
- `OnlineBackup`: Respaldo online
- `DeviceProtection`: Protección de dispositivos
- `TechSupport`: Soporte técnico
- `StreamingTV`: TV por streaming
- `StreamingMovies`: Películas por streaming

**Información de Cuenta**
- `Contract`: Tipo de contrato (Month-to-month/One year/Two year)
- `PaperlessBilling`: Facturación sin papel
- `PaymentMethod`: Método de pago
- `Charges.Monthly`: Cargo mensual
- `Charges.Total`: Cargo total

**Variable Objetivo**
- `Churn`: Cliente se fue (Yes/No)

## 🔧 Proceso ETL

### 1. 📌 Extracción
- Carga de datos desde URL JSON usando `requests` y `pandas`.
- Normalización de estructura JSON anidada.

### 2. 🔧 Transformación
- **Clasificación de variables:**
  - Variables enteras: `customer.tenure`
  - Variables categóricas: 12 variables (género, servicios, métodos de pago, etc.)
  - Variables binarias: 6 variables (churn, partner, dependents, etc.)
  - Variables numéricas: 2 variables (cargos mensuales y totales)
- **Limpieza de datos:**
  - Eliminación de 224 registros con valores vacíos en `Churn` (3% del dataset).
  - Identificación y corrección de inconsistencias en tipos de datos.

### 3. 📈 Análisis Exploratorio de Datos (EDA)
- Análisis estadístico y visualización de las principales variables.
- Identificación de correlaciones y patrones relevantes.

## 📊 Hallazgos y Conclusiones

A partir del análisis exploratorio de datos y la visualización de las principales variables, se identificaron los siguientes hallazgos relevantes sobre el comportamiento de los clientes y su relación con el churn:

1. **Distribución del Churn:**  
   Aproximadamente el 26% de los clientes han abandonado la empresa, mientras que el 71% se mantiene activo. Esto indica una tasa de churn significativa que puede afectar la rentabilidad de la empresa si no se toman medidas.

2. **Relación entre tipo de contrato y churn:**  
   Los clientes con contratos “Month-to-month” (mes a mes) presentan una tasa de churn mucho mayor en comparación con los que tienen contratos de uno o dos años. Esto sugiere que los contratos a largo plazo ayudan a retener clientes.

3. **Servicios de Internet y Churn:**  
   Los usuarios que tienen servicio de internet por fibra óptica muestran una mayor propensión al churn en comparación con los que usan DSL o no tienen servicio de internet. Esto puede estar relacionado con expectativas de calidad o competencia en el mercado de fibra óptica.

4. **Métodos de pago y churn:**  
   El método de pago “Electronic check” está fuertemente asociado con una mayor tasa de churn, mientras que los pagos automáticos con tarjeta de crédito o transferencia bancaria presentan menor abandono.

5. **Cargos mensuales y churn:**  
   Los clientes que pagan cargos mensuales más altos tienden a abandonar la empresa con mayor frecuencia. Esto puede indicar que los clientes más sensibles al precio son más propensos a cancelar el servicio.

6. **Soporte técnico y servicios adicionales:**  
   Los clientes que no cuentan con servicios adicionales como soporte técnico, protección de dispositivos o respaldo online presentan tasas de churn más elevadas. Ofrecer estos servicios puede ser una estrategia para aumentar la retención.

7. **Perfil demográfico:**  
   No se observa una diferencia significativa en el churn entre hombres y mujeres.  
   Los clientes mayores de 65 años (SeniorCitizen) tienen una ligera tendencia a abandonar más que el resto, pero la diferencia no es tan marcada como en otras variables.

8. **Tenencia (tenure):**  
   La mayoría de los clientes que abandonan la empresa tienen una antigüedad menor a 12 meses. A mayor tiempo de permanencia, menor es la probabilidad de churn.

### **Conclusiones Generales**

- El churn está fuertemente influenciado por el tipo de contrato, el método de pago y la cantidad de servicios adicionales contratados.
- Los clientes nuevos y los que pagan mensualmente sin compromiso a largo plazo son los más propensos a abandonar la empresa.
- Se recomienda a la empresa TELECOM X enfocar sus estrategias de retención en ofrecer incentivos para contratos a largo plazo, mejorar la experiencia de los usuarios de fibra óptica y promover servicios adicionales de valor agregado.
- Es fundamental analizar en profundidad los motivos detrás del churn en clientes con cargos mensuales altos y métodos de pago electrónicos para diseñar campañas personalizadas de retención.

## 🛠️ Tecnologías Utilizadas

```python
import pandas as pd
import json
import requests
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
