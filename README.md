# Ecuador · Exportaciones de flores frescas (HS 0603), 2008–2024

Análisis de las tres partidas florícolas de exportación de Ecuador — **rosas** (HS 060311),
**claveles** (HS 060312) y **otras flores frescas** (HS 060319) — cruzando valor exportado con
continente, distancia a Ecuador, PIB del país importador y acuerdos comerciales (FTA/PTA)
vigentes año a año.

**[→ Ver el dashboard interactivo](https://fiorellaluna7lp-commits.github.io/Flores/)**
*(se activa automaticamente 1-2 minutos despues de habilitar GitHub Pages — ver instrucciones abajo)*

## El dashboard interactivo

Página única (`docs/index.html`) con:

- **Mapa mundial clicable** — toca cualquier país y se abre su ficha completa a la derecha:
  valor exportado, distancia a Ecuador, PIB, si tiene FTA/PTA vigente (con la fuente/nota), y un
  mini-gráfico de su evolución 2008-2024.
- **Slider de año** — mueve el control para ver cómo cambia el mapa año a año, o déjalo en
  "Total 2008-24" para ver el acumulado.
- **3 pestañas de producto** — rosas / claveles / otras flores, cada una con su propio mapa,
  KPIs y gráficos.
- **3 gráficos por producto** — barras apiladas por continente-año, y dos dispersiones
  (distancia y PIB) con escala logarítmica.

Corre 100% en el navegador (Plotly.js vía CDN), sin backend — por eso funciona directo en
GitHub Pages.

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
