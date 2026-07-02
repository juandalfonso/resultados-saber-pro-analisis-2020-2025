# Resultados Saber Pro - Análisis 2020-2025

Repositorio del análisis de los resultados de las pruebas Saber Pro 2020–2025 orientado a la Pontificia Universidad Javeriana.

Incluye:

- Notebook de análisis en Python (`Resultados_Saber_Pro_2020_2025.ipynb`)
- Página(s) HTML interactiva(s) con dashboards y herramientas de incentivos
- Metodología y supuestos usados para construir los indicadores

---

## 1. Fuentes de datos

Los datos provienen de los archivos agregados del ICFES para Saber Pro 2020–2025, que contienen información a nivel de:

- Institución
- Programa académico
- Prueba / Competencia
- Percentiles y niveles de desempeño

En el notebook se realiza:

- Lectura de los 6 archivos de Excel (2020–2025)
- Consolidación en un único `DataFrame` (`consolidateddf`)
- Limpieza básica de campos y creación de variables auxiliares (`Year`, `Semester`)

---

## 2. Notebook de análisis

Archivo principal: `notebooks/Resultados_Saber_Pro_2020_2025.ipynb`

Principales bloques de análisis:

1. **Consolidación de la data**
   - Lectura de todos los archivos `Base-de-datos-de-resultados-agregados-de-saber-pro-YYYY.xlsx`
   - Unión en un único `DataFrame` con >2M registros.

2. **Análisis global por institución**
   - Cálculo de la media global (`PROMEDIOGLOBAL`) por institución, año y examen.
   - Ranking nacional de instituciones por año.
   - Posición de la Universidad Javeriana en el ranking para cada año 2020–2025.

3. **Análisis interno por programas Javeriana**
   - Identificación de todos los programas de la Javeriana en la base.
   - Cálculo de media global, cuartiles y variaciones en el tiempo.
   - Clasificación de programas:
     - Top (C4, cuartil superior)
     - Intermedios (C3, C2)
     - Críticos (C1)

4. **Competencias genéricas**
   - Extracción de resultados por competencias (Inglés, Razonamiento Cuantitativo, Lectura Crítica, Competencias Ciudadanas, Comunicación Escrita).
   - Comparación de la Javeriana frente a la media nacional y frente a instituciones líderes.
   - Evolución temporal 2020–2025 por competencia.

5. **Programas prioritarios**
   - Identificación de programas con bajo desempeño relativo y/o deterioro en el tiempo.
   - Criterios combinados de:
     - Cuartil (posición en distribución nacional)
     - Variación de puntaje en años recientes
     - Tamaño del programa (número de estudiantes evaluados)

---

## 3. Página web / dashboards (HTML)

Carpeta principal: `html/`

Archivo clave: `html/saber-pro-javeriana-v2.html`

Secciones principales del dashboard:

1. **Resumen global (Sec 1)**
   - KPIs principales:
     - Evaluados totales Javeriana
     - Media global 2020–2025
     - Posición en ranking nacional por año
     - Número de programas en cuartil superior (C4)
   - Gráficos:
     - Evolución de media global Javeriana vs media nacional.
     - Número de evaluados por año.
     - Posición en el ranking nacional (línea de tiempo).

2. **Comparación externa (Sec 2)**
   - Ranking de instituciones élite (Top 10) por año.
   - Radar de competencias:
     - Javeriana vs U. de los Andes, U. EIA, ICESI, Sabana, Rosario.
   - Tabla comparativa por competencias y ranking por prueba.

3. **Análisis interno por programa (Sec 3)**
   - Top 15 programas por año (barra horizontal).
   - Distribución de programas por cuartil (gráfico donut).
   - Evolución de programas seleccionados en el tiempo.
   - Gráficos tipo burbuja para “programas estrella” y “programas con riesgo”.

4. **Competencias (Sec 4)**
   - Barras comparativas Javeriana vs media nacional por competencia (2025).
   - Serie de tiempo 2020–2025 por competencia.
   - Radar multi-IES filtrable por año.

5. **Programas prioritarios (Sec 5)**
   - Tabla de programas con clasificación C1–C3, variación en el tiempo y nivel de urgencia.
   - Gráfico de burbujas de riesgo (Media actual vs variación 3 años).

6. **Herramienta de incentivos (Sec 6)**
   - **Incentivos por programa**:
     - Slider de percentil para seleccionar el corte (P50–P99).
     - Cálculo dinámico:
       - Número de programas que superan el umbral.
       - Porcentaje de programas elegibles.
       - Gráfico de barras con los programas elegibles y sus medias.
   - **Incentivos por estudiantes**:
     - Slider de percentil top (P90–P99.9).
     - Uso de distribución normal de `PROMEDIOGLOBAL` (μ=170.2, σ=19.3) para:
       - Estimar puntaje mínimo del percentil.
       - Estimar número de estudiantes Javeriana en ese percentil.
       - Graficar curva normal con zona de incentivo sombreada.
   - **Zona de carga de Excel**:
     - Drag & drop para subir el nuevo archivo de resultados agregados del ICFES.
     - Mensaje de confirmación y diseño preparado para que, en el futuro, el backend lea este archivo y actualice los gráficos.

---

## 4. Arquitectura de archivos propuesta

```text
resultados-saber-pro-analisis-2020-2025/
├── README.md
├── notebooks/
│   └── Resultados_Saber_Pro_2020_2025.ipynb
├── html/
│   ├── saber-pro-javeriana-v1.html
│   └── saber-pro-javeriana-v2.html  # versión principal del dashboard
└── index.html  # copia o referencia al HTML a publicar como sitio
```
