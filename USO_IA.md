# Declaración de uso de inteligencia artificial

- **Herramienta:** ChatGPT (Codex), con herramientas de hojas de cálculo, consulta de fuentes y compilación LaTeX. En la preparación de estos archivos no se utilizó Copilot.
- **Propósito:** apoyar la organización del proyecto, implementar las ecuaciones indicadas en la consigna, hacer explícitas las unidades y verificaciones, preparar la figura y redactar una nota técnica comprensible.
- **Consulta o tarea realizada:** se entregaron las instrucciones del Hito 1 y los archivos originales. Se solicitó desarrollar la comparación carga–deflexión y organizar las entradas, el análisis, las figuras y el reporte según la estructura requerida.
- **Contenido incorporado:** estructura de carpetas, copias de trabajo en Excel, fórmulas, gráfico editable, exportación de resultados, figura PNG, fuentes LaTeX y BibTeX, borrador de la nota, README e instrucciones de entrega. Los datos originales no fueron generados ni corregidos por la IA.

## Procedimiento de verificación realizado durante la preparación

1. Se contrastaron L, b, h y E con la hoja `Parametros`, B4:B7, y las nueve observaciones con el CSV original. Las copias de los siete archivos recibidos se compararon byte por byte y se registraron sus huellas SHA-256.
2. Se contrastó la ecuación de la deflexión central con Roylance (2000), ejemplo 1, y Wierzbicki (2013), sección 5.3, en fuentes originales de MIT. Se incluyeron los documentos en BibTeX. ChatGPT no se citó como fuente técnica.
3. Se revisaron las conversiones kN→N, GPa→N/m² y m→mm, y la consistencia dimensional. Se calculó la fila de 40 kN mediante otra conversión completa a N y mm: el resultado fue 2,00 mm.
4. Se compararon los resultados de las nueve filas con un cálculo separado durante la preparación. En carga cero se verificó `n.a.` para cocientes no definidos. Se comprobó el intervalo de δmed/P y la media relativa de 1,880357 %.
5. Se modificó temporalmente E de 25 a 50 GPa para comprobar el recálculo: la deflexión teórica a 40 kN pasó de 2 a 1 mm. Se restauraron los parámetros originales antes de guardar.
6. Se revisaron los rangos de las dos series del gráfico, las unidades y las nueve cargas. La figura del reporte usa valores exportados de las mismas celdas.
7. Se compiló la nota localmente con pdfLaTeX y BibTeX y se revisaron visualmente sus páginas y referencias. La apertura en Excel y la compilación en la cuenta de Overleaf del estudiante quedan pendientes de revisión personal.

## Cambios, correcciones y decisiones

Se conservó la geometría y E entregados, sin ajustarlos para hacer coincidir los datos. Se definió expresamente la diferencia relativa respecto del valor teórico y se excluyó únicamente el cociente a carga cero. No se atribuyeron las desviaciones a causas experimentales reales, ya que los datos son sintéticos. Se verificaron el eje numérico del gráfico, la fila final y la legibilidad de las cifras. No se fabricó un historial ni un hash de GitHub.

La plantilla de Overleaf no estaba entre los adjuntos; se creó una fuente independiente. La generación asistida de los archivos no equivale a una ejecución manual realizada por el estudiante. El flujo de continuación utiliza Excel y LaTeX, sin scripts de análisis.

## Responsabilidad y revisión del estudiante

**Estado:** la revisión personal y la publicación en GitHub están pendientes. No se declara que el estudiante haya ejecutado las verificaciones automatizadas ni que ya haya defendido el contenido.

Antes de la entrega, el estudiante debe comprobar las fórmulas en Excel, repetir al menos la comprobación de 40 kN, recompilar en Overleaf y verificar que entiende la medida relativa y los límites del modelo. Solo después de realizar esa revisión corresponde registrar su conformidad con la declaración de la plantilla: «Declaro comprender y poder defender el contenido entregado».
