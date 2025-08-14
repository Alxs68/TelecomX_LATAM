# TelecomX — Evasión de Clientes (Churn) — ETL y Exploración

## 1) Objetivo
Preparar un dataset **limpio** y **documentado** de churn (evasión de clientes) para una siguiente etapa de **Machine Learning**.  
La variable objetivo es `churn` con valores **YES/NO**; los vacíos se tratan como **NaN** y se reservan para *scoring* posterior.

---

## 2) Notebooks incluidos

  Carga directa desde GitHub (`TelecomX_Data.json`) con `pd.json_normalize`, ETL básico y visualizaciones simples.

---

## 3) Requisitos
- Python 3.9+  
- Jupyter / Colab  
- Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`, `requests`

Instalación rápida (local):
```bash
python -m venv .venv && source .venv/bin/activate  # en Windows: .venv\Scripts\activate
pip install -U pip
pip install pandas numpy matplotlib seaborn plotly requests jupyter
jupyter notebook
```

---

## 4) Cómo ejecutar
### Opción A — Colab
1. Sube el notebook `TelecomX_ETL_Churn_Clientes (Extra Correlaciones).ipynb` a Colab.  
2. Ejecuta todas las celdas. La carga usa el `RAW_URL` ya configurado para `TelecomX_Data.json`.

### Opción B — Local
1. Abre el notebook en Jupyter.  
2. En la celda de extracción verifica/ajusta:
   ```python
   RAW_URL = "https://raw.githubusercontent.com/Alxs68/TelecomX_LATAM/main/TelecomX_Data.json"
   ```
3. Ejecuta las celdas en orden (de arriba hacia abajo).

---

## 5) Flujo ETL implementado
1. **Extracción**: lectura de JSON remoto desde GitHub y normalización con `pd.json_normalize(...)`.  
2. **Exploración inicial**: columnas, tipos y nulos.  
3. **Limpieza**:
   - Estandarización de `churn` a **YES/NO** (otros valores → `NaN`).
   - Mapeo de binarios comunes (SI/NO/TRUE/FALSE) a `0/1` en otras columnas cuando aplique.
   - Eliminación de duplicados exactos.
4. **Conversión numérica**:
   - Corrección de formatos con símbolos (`$`, `%`) y separadores de miles/decimales tipo `1.234,56` o `1,234.56`.
   - Conversión a `float` cuando **≥90%** de los valores de la columna pueden interpretarse como número.
5. **Transformación**:
   - Separación en `df_ml` (registros con etiqueta `YES/NO`) y `df_score` (etiqueta vacía).
   - Creación de `churn_flag` (`YES→1`, `NO→0`).
   - Detección de columnas **numéricas** y **categóricas** (evitando tratar como numéricas los ID con cardinalidad ~N).
6. **Selección automática**: *Top 2* numéricas (|r de Pearson| vs `churn_flag`) y *Top 2* categóricas (mayor **spread** de tasa de churn).

---

## 6) Visualizaciones generadas
- **Boxplots** de las *Top 2* **numéricas** por clase (`YES/NO`).  
- **Barras** de tasa de churn para las *Top 2* **categóricas**, con eje en **%** y línea de **baseline** (tasa global).  
- **Un gráfico interactivo (Plotly)** para la categórica más influyente.  
- *(Opcional en el notebook)*: **Matriz de correlación** de numéricas (triángulo inferior).

---

## 7) Salidas del ETL
- **`TelecomX_churn_ML_ready.csv`**  
  Dataset **listo para modelar** (solo filas con etiqueta YES/NO), incluye `churn_flag` y las columnas limpias.
- **`TelecomX_churn_unlabeled_to_score.csv`**  
  Registros con `churn` vacío (NaN), para **scoring** posterior con el modelo entrenado.

---

## 8) Decisiones de datos
- `churn` vacío → **no se imputa** ni se crea clase “UNKNOWN”; se **excluye** del entrenamiento y se guarda en `*_unlabeled_to_score.csv`.
- Mapeo binario **SI/NO/TRUE/FALSE** → `0/1` cuando la columna completa es compatible.
- Conversión numérica **tolerante** a formatos con símbolos y separadores internacionales.
- Normalización básica de texto en categóricas (espacios y mayúsculas).

---

## 9) Próximos pasos (sugeridos para ML)
- División **estratificada** `train/valid/test` según `churn_flag`.
- Tratamiento del **desbalance** (si aplica): `class_weight`, `SMOTE` o *undersampling*.
- **Codificación** de categóricas (One-Hot / Target Encoding, según el modelo).
- **Escalado** de numéricas (si el algoritmo lo requiere).
- Modelos base: **Regresión Logística** y **Árboles/Boosting** (comparar AUC/PR, F1 y *calibración*).

---

## 10) Checklist de entrega
- [ ] Notebook ejecuta de inicio a fin sin errores.  
- [ ] Se visualizan 3–4 gráficos clave.  
- [ ] Se generan `TelecomX_churn_ML_ready.csv` y `TelecomX_churn_unlabeled_to_score.csv`.  
- [ ] Se explican en el informe las **decisiones de limpieza** y **qué variables** se usarán en ML.
