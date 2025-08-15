# 📊 Proyecto TelecomX - Análisis de Churn de Clientes

## 📌 Descripción
Este proyecto realiza un **análisis exploratorio, limpieza, transformación y visualización** de datos de clientes para comprender los factores que más influyen en la tasa de cancelación (*churn*).  
Todo el código, variables y comentarios están en **español**, pensado para que sea comprensible por analistas y directivos no técnicos.

## 🎯 Objetivos
1. Cargar datos desde fuente externa (GitHub o archivo local).
2. Traducir y estandarizar los nombres de columnas al español.
3. Explorar el conjunto de datos para detectar patrones.
4. Analizar las variables numéricas y categóricas más influyentes en el *churn*.
5. Visualizar resultados con **Matplotlib**, **Seaborn** y **Plotly**.
6. Generar conclusiones y recomendaciones accionables.

## 📂 Flujo del análisis
1. **Carga y traducción de datos**: Lectura desde JSON y renombrado de columnas.
2. **Exploración inicial**: Estadísticas descriptivas y visualización general.
3. **Limpieza y transformación**:
   - Eliminación de duplicados.
   - No se imputan valores vacíos en la variable `churn_flag` para mantener integridad del análisis.
4. **Análisis exploratorio detallado**:
   - Variables numéricas clave: `ANTIGUEDAD_MESES`, `CARGO_MENSUAL`, etc.
   - Variables categóricas clave: `TIPO_CONTRATO`, `METODO_PAGO`, `TIPO_INTERNET`.
5. **Visualizaciones**:
   - Gráficos de barras, pastel, dispersión y correlaciones.
   - Visualización interactiva con Plotly para las variables más influyentes.
6. **Informe final**:
   - Resumen de hallazgos.
   - Recomendaciones para reducir la tasa de *churn*.

## 📊 Principales hallazgos
- Mayor tasa de *churn* en clientes con contratos **mensuales**.
- Clientes con **cargo mensual más alto** tienden a abandonar más.
- El método de pago **electrónico** muestra menor *churn* frente a pagos físicos.
- Servicios de internet de tipo **DSL** presentan más cancelaciones que fibra óptica.

## 📌 Recomendaciones accionables
1. **Fidelización**: Diseñar campañas de retención para clientes con contrato mensual, ofreciéndoles planes anuales con beneficios.
2. **Optimización de precios**: Revisar tarifas para clientes con alto cargo mensual y alto *churn*.
3. **Incentivar pago electrónico**: Promociones o descuentos por uso de pago digital.
4. **Mejorar infraestructura DSL**: Migrar clientes DSL a fibra óptica donde sea posible.

## 🛠️ Tecnologías utilizadas
- Python 3.x
- Pandas
- Matplotlib
- Seaborn
- Plotly


