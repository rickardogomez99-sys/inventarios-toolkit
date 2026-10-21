# Inventarios Toolkit

Herramienta interna para digitalizar los conteos y ajustes de inventario de un CEDIS que trabaja con **Microsip**. Reemplaza varias macros de Excel (VBA) con una sola página web que corre en el navegador y genera los archivos de importación a Microsip.

> Es una herramienta interna, **no un SaaS**: no tiene backend, no usa servidor propio y no guarda datos.

## Qué incluye

Un solo archivo HTML con un menú lateral y siete herramientas:

- **Verdura · Ajuste mensual**
  - Sube el reporte de existencias de Microsip.
  - Busca cada verdura por nombre o código (también con pistola de código de barras).
  - Captura el peso real y calcula **Sistema − Peso**: si falta es Salida, si sobra es Entrada.
  - Genera los archivos de Salidas y Entradas solo con lo que se pesó.
  - Conserva los modos "Uno por uno" y "Vista de tabla" como respaldo.
- **Análisis de Verdura**
  - Sube la relación de inventario de mermas (uno o varios archivos, se suman).
  - Muestra el Top 5, 10 o 15 de verduras por costo de pérdida, con las unidades perdidas al lado.
  - Incluye fila de VARIOS, TOTAL y gráfica Pareto (costo y % acumulado).
  - Permite quitar artículos como **excepciones** (ajuste atrasado o justificable): la lista se recorre y los totales se recalculan.
  - Descarga un Excel con el Top, el detalle y las excepciones.
- **Miércoles · Rectificación**
  - Recuenta solo los artículos con Salidas mayores a 6.
  - Clasifica cada producto como MERMA, Ajuste ENTRADA o NO impacta.
  - Calcula el costo de la merma y genera el archivo de Entrada.
- **Negativos**
  - Carga el reporte de artículos con existencia negativa.
  - Captura la existencia real (pasillo y bodega) y genera el archivo de Entradas.
- **Mermas de Tarima**
  - Registra con pistola de código de barras los artículos dañados o caducados en tablas separadas.
  - Descarga cada tabla en su formato.
- **Análisis de Mermas**
  - Sube los reportes mensuales de Merma Caducidad y Merma Daño.
  - Genera el análisis Top 5/10 + Varios con gráfica Pareto.
- **Inventario Mensual**
  - Sirve para inventarios externos (SAM'S, USA, Walmart u otros).
  - Compara Real contra Teórico y genera Entrada o Salida según el signo de la diferencia.

## Cómo usarlo

- Descarga el archivo HTML del repositorio.
- Ábrelo con doble clic en tu navegador (Chrome, Edge o Firefox).
- Elige un proceso en el menú lateral y sigue los pasos.
- Descarga los archivos generados e impórtalos a Microsip como siempre. **La importación sigue siendo manual.**

## Cosas a tener en cuenta

- **Necesita internet al abrirse** para cargar las librerías [SheetJS](https://sheetjs.com/) (leer y escribir Excel) y [Chart.js](https://www.chartjs.org/) (gráficas) desde cdnjs, y la tipografía Inter desde Google Fonts.
- **Los datos no salen de tu computadora.** Todo se procesa en el navegador; nada se sube a un servidor.
- **No guarda la captura.** Si cierras o recargas la pestaña se pierde lo capturado (el navegador avisa antes de cerrar). Descarga los archivos antes de salir.
- **Formato de los archivos para Microsip:** fila 1 vacía, clave del artículo en la columna A y cantidad en la columna B.
- **No subas reportes reales** (existencias, mermas, costos) a este repositorio: es público y esos datos son de la empresa.

## Tecnología

- HTML, CSS y JavaScript sin framework, en un solo archivo.
- [SheetJS](https://sheetjs.com/) 0.18.5 para leer y generar `.xlsx`.
- [Chart.js](https://www.chartjs.org/) 4.4.4 para las gráficas Pareto.
- Diseño propio: verde bosque `#1B4332` y naranja `#F2994A` (colores del logo), tipografía Inter, animaciones solo con CSS y Web Animations API que respetan la opción "reducir movimiento" del sistema.

## Historial de versiones

- **v1.3**
  - Verdura pasa a ser **Ajuste mensual** con el nuevo modo **Buscar y pesar**.
  - Se corrigió el desborde en pantallas de celular.
- **v1.2**
  - Diseño nuevo con animaciones (solo visual, sin cambios de lógica).
- **v1.1**
  - Nueva sección **Análisis de Verdura** con excepciones.
  - Botón para terminar antes la captura de Verdura.
  - Arreglos: el scroll ya no salta al inicio al capturar en tablas, el buscador restaura la lista al borrar el texto y una baja con existencia 0 ya no genera una Salida vacía.
  - Aviso del navegador antes de cerrar con captura sin descargar.
  - Icono propio en la pestaña del navegador.
- **v1.0**
  - Versión base con los procesos originales.
