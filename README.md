# inventarios-toolkit

> Standalone web app that digitizes recurring warehouse inventory processes and generates ready-to-import files for **Microsip ERP**.
> Single HTML file · No backend · No installation · Runs entirely in the browser.

🇲🇽 [Versión en español más abajo](#-versión-en-español)

---

## The problem

In a distribution center (CEDIS), several inventory processes (weekly produce counts, negative-stock corrections, damaged/expired goods, monthly audits) were handled with **Excel macros (VBA)**: one file per process, hard to maintain, and hard for new employees to pick up.

Each process follows the same pattern: load an ERP report → capture the physical count → compare against the system → generate an Entrada/Salida file for the ERP.

## The solution

One HTML file with a sidebar to switch between processes. All of them share the same engine:

1. **Load** the report exported from Microsip (.xlsx)
2. **Capture** the real physical count
3. **Calculate** differences (System − Real)
4. **Generate** the import file (Entrada / Salida) in the exact format the ERP expects

## Processes

| Process | What it does |
|---|---|
| **Lunes · Verdura** | Weekly produce count. Cross-checks the Microsip stock report against a catalog of ~165 products and generates Entrada/Salida files. |
| **Miércoles · Rectificación** | Re-counts only items with high outflows. Classifies each product as *Merma* / *Ajuste Entrada* / *No impacta* and calculates shrinkage cost. |
| **Negativos** | Fixes items with negative stock in the system by capturing real stock and generating an Entrada file. |
| **Mermas de Tarima** | Fast logging of damaged and expired goods using a barcode scanner, in separate Daño / Caducidad tables. |
| **Análisis de Mermas** | Monthly shrinkage report: Top 5/10 + "Varios", with a Pareto chart (cost + cumulative %). |
| **Inventario Mensual** | Generic external-inventory process (e.g. SAM'S, USA, Walmart). Compares Real vs. Theoretical and generates Entrada or Salida depending on the sign of the difference. |

## Tech stack

- Vanilla **JavaScript**, HTML and CSS (single file)
- [SheetJS (xlsx)](https://sheetjs.com/) for reading and writing Excel files
- [Chart.js](https://www.chartjs.org/) for the Pareto charts
- UI inspired by SAP Fiori (Inter typeface, dense layout, sidebar navigation)

## How to use

1. Download `INVENTARIOS.html`
2. Open it in any modern browser (Chrome, Edge, Firefox, Brave)
3. Pick a process from the sidebar and follow the steps

> Internet is needed only to load the two libraries from a CDN. Data is processed locally and never leaves your computer.

## Design decisions

- **Single file, no server:** easy to share and to run on any workstation.
- **Business rules built in:** for example, in the Wednesday process, if Real < Salidas the difference is treated as *merma* (with cost) even though the ERP adjustment is an Entrada.
- **Built to be handed over:** the goal is that warehouse staff can operate it without technical support.

## Screenshots

_Add screenshots here (Home, a capture screen, the Pareto chart)._

## Changelog

- **v1.1** – Fix: product code for PLATANO OFERTA now keeps leading zeros (`00230`) to match Microsip.
- **v1.0** – Initial version.

## Author

**Ricardo Gómez** – Industrial Maintenance Engineer · Data Analyst / Inventory Specialist
[GitHub](https://github.com/rickardogomez99-sys)

---

## 🇲🇽 Versión en español

**inventarios-toolkit** es una herramienta web independiente que digitaliza los procesos recurrentes de inventario de un CEDIS y genera los archivos de importación para **Microsip ERP**. Es un solo archivo HTML, sin servidor ni instalación.

### El problema

Los procesos de inventario (conteo semanal de verdura, corrección de negativos, mermas, inventarios mensuales) se manejaban con **macros de Excel (VBA)**: un archivo por proceso, difícil de mantener y de enseñar a nuevo personal.

### La solución

Un solo archivo con un menú lateral para elegir el proceso. Todos comparten el mismo flujo: **cargar reporte → capturar conteo real → calcular diferencias → generar archivo de Entrada/Salida** para Microsip.

### Procesos incluidos

- **Lunes · Verdura:** conteo semanal contra catálogo de ~165 productos.
- **Miércoles · Rectificación:** recuento de artículos con salidas altas; clasifica merma y calcula costo.
- **Negativos:** corrige artículos con existencia negativa.
- **Mermas de Tarima:** captura de daño y caducidad con pistola de código de barras.
- **Análisis de Mermas:** reporte mensual Top 5/10 con gráfica Pareto.
- **Inventario Mensual:** inventarios externos (SAM'S, USA, Walmart u otros).

### Cómo usarla

1. Descarga `INVENTARIOS.html`
2. Ábrelo en tu navegador
3. Elige un proceso en el menú lateral y sigue los pasos

Los datos se procesan localmente en el navegador; no se envían a ningún servidor.
