# Ecuador · Exportaciones de flores frescas (HS 0603), 2008–2024

Análisis de las tres partidas florícolas de exportación de Ecuador — **rosas** (HS 060311),
**claveles** (HS 060312) y **otras flores frescas** (HS 060319) — cruzando valor exportado con
continente, distancia a Ecuador, PIB del país importador y acuerdos comerciales (FTA/PTA)
vigentes año a año.

**[→ Ver el dashboard interactivo](https://fiorellaluna7lp-commits.github.io/Flores/)**
*(se activa automaticamente 1-2 minutos despues de habilitar GitHub Pages — ver instrucciones abajo)*

## The interactive dashboard — "Bloom Atlas"

Single-screen, horizontal BI-style layout (`docs/index.html`), in English, saturated
tropical/floral palette (fuchsia, jungle green, marigold, violet on a deep forest-green header):

- **Big interactive world map** — spans the full width at ~560px tall for easy country
  selection. Click any country for its full profile (value, distance, GDP, FTA/PTA status +
  source note, mini trend line 2008–2024).
- **Year filter** (top bar dropdown) — isolate the whole dashboard (map, KPIs, charts, rankings)
  to a single year, or view "All years 2008–24" accumulated.
- **Agreement filter** — show only countries with an **FTA**, only **PTA**, **no agreement**, or
  all — the map and every chart update to match, with live counts (FTA / PTA / none) shown above
  the map.
- **Nominal $ / Real (2024) $ toggle** — inflation-adjusts every KPI, chart and the map using
  U.S. CPI-U annual averages (BLS), rebased to 2024 dollars.
- **Fullscreen mode** — the ⛶ button uses the browser's Fullscreen API so the dashboard fills the
  entire screen with no browser chrome, ideal for presenting.
- **Click-to-zoom charts** — click the continent donut or either scatter plot to open it enlarged
  in a modal. Click a second chart while the modal is open and both appear **side by side**.
- **Total Purchases 2008–2024 — All Products Compared** — full-width overlay line chart showing
  roses vs. carnations vs. other flowers across the whole period, active product highlighted
  (replaces the old top-countries pie chart).
- **"What is this product?" card** — description + illustration for the selected tariff code.
- **Top destination countries** ranked list, tagged FTA/PTA.
- **Growth trend arrow** on the Total Exported KPI (only shown in "All years" view).

Runs 100% client-side (Plotly.js via CDN, no backend) — works directly on GitHub Pages.

### On the inflation adjustment

Nominal export values are in the dollars of the year they were recorded — $1 in 2008 bought more
than $1 in 2024. The **Real $ (2024)** toggle multiplies every year's value by
`CPI_2024 / CPI_year` (U.S. CPI-U annual averages) so all 17 years are comparable in constant
purchasing power. This raises older years' figures and gives a truer picture of growth than the
raw nominal numbers.

## Qué responde este análisis

1. **¿Exportamos más según el continente del comprador?**
2. **¿Exportamos más a países cercanos a Ecuador?**
3. **¿Exportamos más a países con mayor PIB?**

Resultado consistente en las tres partidas: la **distancia no explica el volumen** exportado
(correlación cercana a 0), mientras que el **PIB del país importador sí** (correlación 0.55–0.81).

## Estructura del repositorio

```
├── docs/                    # Dashboard interactivo (GitHub Pages sirve esta carpeta)
│   ├── index.html           # Página con Plotly.js, un tab por partida arancelaria
│   └── data.json            # Datos ya agregados (continente×año, resumen por país, correlaciones)
├── excel/                   # Libros de Excel fuente, con fórmulas nativas
│   ├── Ecuador_Rosas_060311_2008-2024_FORMULAS.xlsx
│   ├── Ecuador_OtrasFlores_060319_2008-2024_FORMULAS.xlsx
│   └── Ecuador_Claveles_060312_2008-2024_FORMULAS.xlsx
└── README.md
```

## Los archivos Excel

Cada libro trae, por hoja:

| Hoja | Contenido |
|---|---|
| `Ref_Continente` | País → continente (entrada editable) |
| `Ref_Acuerdos` | País → tipo de acuerdo (FTA/PTA), año de entrada en vigor, tarifa % (entrada editable) |
| `Datos` | Panel país-año 2008-2024. Continente/FTA/PTA/Tariff son **fórmulas VLOOKUP** contra las hojas de referencia |
| `Continente_x_Anio` | `SUMIFS` — exportación por continente y año |
| `Resumen_Pais` | `SUMIF`/`AVERAGEIF`/`SUMIFS` — totales por país |
| `Analisis` | `CORREL()` — las correlaciones que responden las 3 preguntas |
| `Graficos` | Los 3 gráficos nativos de Excel (barras apiladas, dos dispersiones con línea de tendencia) |

Edita cualquier celda azul en `Ref_Continente` o `Ref_Acuerdos` y todo el libro se recalcula solo.

## Fuentes

- Datos comerciales: UN Comtrade (vía Google Sheets del usuario).
- FTA/PTA: SICE-OEA ([sice.oas.org/ctyindex/ecu](http://www.sice.oas.org/ctyindex/ecu)),
  Ministerio de Producción, Comercio Exterior e Inversiones de Ecuador
  ([produccion.gob.ec](https://www.produccion.gob.ec)).

## Publicar el dashboard con GitHub Pages

1. Sube este repo a GitHub (ver comandos abajo).
2. En GitHub: **Settings → Pages → Source → Deploy from a branch → main /docs**.
3. En 1-2 minutos queda publicado en `https://TU-USUARIO.github.io/TU-REPO/`.

## Comandos para subirlo

```bash
git remote add origin https://github.com/fiorellaluna7lp-commits/Flores.git
git branch -M main
git push -u origin main
```
