# Análisis de ventas — Impacto de campaña publicitaria

Este proyecto es la tesis de maestría de nuestro equipo en Big Data e Inteligencia de Negocios. Queríamos saber cuánto vendió la empresa gracias a su campaña publicitaria, y cuánto hubiera vendido de todas formas sin ella.

Para responderla usamos datos reales de ventas diarias de una empresa de bebidas alcohólicas — dos años de transacciones, más de 10,000 registros — y construimos modelos que estiman cómo se habrían comportado las ventas sin la campaña. La diferencia entre esa proyección y lo que realmente pasó es el impacto incremental.

---

## ¿Qué hay en este repositorio?

- **SQL** — modelo de base de datos en MySQL (esquema estrella con tabla de ventas, dimensión de fechas y tipos de cambio) y 15 consultas analíticas con window functions, CTEs y JOINs
- **Python / Notebook** — limpieza de datos, análisis exploratorio y comparación de 6 modelos de series temporales
- **Streamlit app** — dashboard interactivo donde puedes cambiar las fechas de campaña y ver el impacto estimado en tiempo real
- **CSVs** — los datos procesados listos para cargar

---

## Resultados principales

La campaña analizada duró de junio a septiembre de 2023. Usando Prophet como modelo de referencia:

- Ventas reales durante la campaña: **$2,331,804 USD**
- Ventas proyectadas sin campaña: **$1,459,168 USD**
- Impacto incremental estimado: **+$872,635 USD (+59.8%)**
- ROAS estimado: **9.70**

También corrimos PCA sobre las ventas por marca y se ve claramente cómo cambia el patrón de compra durante la campaña — no solo suben las ventas en general, sino que cambia qué marcas jalan más.

---

## Modelos que probamos

| Modelo | RMSE |
|---|---|
| Prophet | 11,099 |
| Exponential Smoothing | 12,427 |
| ARDL | 12,840 |
| SARIMA | 13,166 |
| Event Study | 14,854 |
| Naive | 14,922 |

Nos quedamos con Prophet por tener el menor error, aunque el análisis completo con todos los modelos está en el notebook.
