# 📊 Telecom X — Evasión de Clientes (EDA + ETL)
Proyecto de análisis exploratorio y preparación de datos para entender la **evasión de clientes (churn)** en Telecom X.  
Trabajo realizado por un perfil **principiante** en ciencia de datos (con apoyo de IA), usando **Python** para ETL, EDA y visualizaciones.

---

## 🎯 Objetivo
- **Comprender** qué factores se asocian con la cancelación del servicio.
- **Preparar** los datos (ETL) para análisis y futuros modelos.
- **Comunicar** hallazgos con visualizaciones simples y conclusiones accionables.

---

## 🧠 Qué practiqué
- Extracción de datos desde una **URL (JSON)**.
- **Limpieza** y **transformación** básica (strings, nulos, coherencias).
- **Estandarización** (banderas 0/1, columnas en español).
- Análisis exploratorio (**EDA**) con tablas y gráficos.
- Elaboración de un **informe** claro y breve con insights y recomendaciones.

---

## 📦 Datos
- Fuente: archivo JSON (simula una API) publicado en GitHub.
- Estructura: información de clientes (contrato, servicios, cobros, etc.) y etiqueta **`Churn`**.
- Nota: En este proyecto traté el valor vacío de `Churn` como **"Desconocido"** (no adivino Yes/No).

> URL usada en el notebook:  
> `https://raw.githubusercontent.com/Alxs68/TelecomX_LATAM/main/TelecomX_Data.json`

---

## 🗂️ Estructura del Notebook
Celdas principales (paso a paso, nivel principiante):

1. **📥 Extracción**  
   Carga desde URL y normalización del JSON.

2. **🧹 Limpieza & Coherencia → `df_clean`**  
   - Quitar espacios (`strip`)  
   - `Churn`: `'' → "Desconocido"`  
   - Unificar `"No phone/internet service" → "No"`  
   - Reglas simples (si no hay internet/teléfono, complementos = "No")  
   - Conversión a numérico: cargos y `tenure`  
   - Deduplicar por `customerID` (si hay)

3. **🧱 Estandarización + 🇪🇸 Traducción → `df_std`, `df_std_full_es`**  
   - Banderas `_flag` = 0/1 desde Yes/No  
   - `Cuentas_Diarias` desde cargo mensual  
   - Traducción **1:1** de todas las columnas a **español**

4. **📈 Análisis descriptivo**  
   - `describe()`, medianas, métricas por `churn`  
   - Distribución de categóricas clave

5. **📊 Distribución de churn**  
   - Barras (Yes/No/Desconocido)  
   - Torta (solo Yes/No)

6. **🗂️ Churn por categorías**  
   - Tasas de churn por `tipo_contrato`, `metodo_pago`, `tipo_internet`, etc.  
   - Barras de tasa y conteos apilados

7. **📝 Informe final (auto)**  
   - Introducción, limpieza, EDA, conclusiones, recomendaciones  
   - Gráficos de apoyo y **tabla de brecha relativa** en numéricos

---

## ▶️ Cómo ejecutar (Colab recomendado)
1. Abre el notebook en **Google Colab**.
2. Ejecuta las celdas **en orden** (1 → 7).
3. Requisitos (Colab ya trae casi todo):
   ```python
   # Solo si quieres gráficos opcionales:
   # !pip install seaborn plotly --quiet
