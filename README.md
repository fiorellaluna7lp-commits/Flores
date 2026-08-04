# Ecuador · Exportaciones de flores frescas (HS 0603), 2008–2024

Análisis de las tres partidas florícolas de exportación de Ecuador — **rosas** (HS 060311),
**claveles** (HS 060312) y **otras flores frescas** (HS 060319) — cruzando valor exportado con
continente, distancia a Ecuador, PIB del país importador y acuerdos comerciales (FTA/PTA)
vigentes año a año.

**[→ Ver el dashboard interactivo](https://fiorellaluna7lp-commits.github.io/Flores/)**
*(se activa automaticamente 1-2 minutos despues de habilitar GitHub Pages — ver instrucciones abajo)*

## The interactive dashboard — "Bloom Atlas"

A single, big **vertical-scrolling page** (`docs/index.html`) in a saturated tropical/floral
palette (fuchsia, jungle green, marigold, violet on a deep forest header). The **Bloom Atlas**
title banner scrolls away with the page, but the **filter bar stays pinned** (sticky) at the top
as you scroll, so Product / Values / Year / Agreement / Fullscreen are always within reach.

- **KPI ring row** — total exported, top buyer, distance/GDP correlation, with a growth-trend arrow.
- **Product picker with an "All Products" option** — switch between roses / carnations / other
  flowers, or select **All Products** to see the three tariff codes merged into one combined view
  (map, KPIs, charts and correlations all recompute over the sum of the three).
- **A big clickable world map** (640px tall, full width) — colored on a **single-hue scale**
  (light = low export value, deep fuchsia = high export value) instead of a multi-color scale, so
  it reads at a glance. **Hover** any country to see its export value and FTA/PTA status right in
  the tooltip (e.g. "Russia $249,393 · FTA: No / PTA: No"); **click** it for the full profile in
  the side panel (value, distance, GDP, FTA/PTA + source note, mini trend line). The panel stays
  small when empty instead of a big blank box.
- **Agreement filter** (top bar) — show only countries with an active FTA, only PTA, only
  "no agreement", or all; live counts shown above the map.
- **Year filter** (top bar dropdown) — isolate the whole dashboard to a single year, or view all
  years accumulated.
- **Total Purchases 2008–2024 — All Products Compared** — all 3 products' yearly export value
  overlaid on one chart, active product highlighted.
- **"What is this product?"** — description + illustration for the selected tariff code.
- Continent donut, distance scatter, GDP scatter.
- Top destination countries ranked list, tagged FTA/PTA.
- **QR code** in the last grid slot — scan to open the live dashboard on a phone; the whole page
  is mobile-responsive (cards stack, map and charts resize) so it works the same on a small screen.
  On phones the filter bar collapses behind a single **⚙ Filters** button (with a small badge
  showing any active Year/Agreement/Real-$ filter) instead of taking over the screen.
- **Fullscreen button** — uses the browser's Fullscreen API so the address bar and browser chrome
  are hidden while presenting.
- **Nominal $ / Real (2024) $ toggle** — inflation-adjusts every KPI, chart and the map using
  U.S. CPI-U annual averages (BLS), rebased to 2024 dollars.

Runs 100% client-side (Plotly.js via CDN, no backend) — works directly on GitHub Pages.

### Data cleanup

- Non-country Comtrade categories ("Areas, nes", "Free Zones", "Other Asia, nes",
  "Br. Indian Ocean Terr.", "Netherlands Antilles (...2010)") are excluded from every chart, the
  map, the rankings and the correlations — only real destination countries are counted.
- Ukraine's distance to Ecuador was corrected to **11,500 km** (the source sheet had a truncated
  "11.00" that parsed as 11 km).

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
