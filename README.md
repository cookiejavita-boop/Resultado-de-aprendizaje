# Hito 1: carga y deflexión de una viga

**Estudiante:** Benjamín Vergara. **Caso:** viga simplemente apoyada, sección rectangular y carga puntual centrada. **Datos:** sintéticos, proporcionados para la actividad docente.

El proyecto compara las nueve deflexiones del CSV con el modelo lineal elástico de Euler–Bernoulli. El análisis se realiza mediante fórmulas editables en Excel. La nota técnica está escrita en LaTeX y las referencias se gestionan con BibTeX.

## Organización

| Ruta | Función |
|---|---|
| `README.md` | Procedimiento, unidades, supuestos y continuidad del trabajo. |
| `data/datos_viga.csv` | Observaciones originales, sin modificaciones. |
| `data/parametros_viga.xlsx` | Geometría y módulo originales, sin modificaciones. |
| `analysis/analisis_viga.xlsx` | Copias de las entradas, fórmulas, gráfico y verificaciones. |
| `figures/carga_deflexion.png` | Figura de ambas series, a 300 ppp. |
| `report/main.tex` | Fuente de la nota técnica. |
| `report/referencias.bib` | Dos referencias técnicas verificadas. |
| `report/nota_tecnica.pdf` | Nota compilada para esta versión de las entradas. |
| `USO_IA.md` | Asistencia utilizada, contenido incorporado y verificación. |

Se añaden `data/esquema_viga.png` y `data/README_datos.md` como material original del caso. `docs/originales/` conserva el checklist, la plantilla de declaración de IA y la captura recibida. `docs/ORIGINALES.sha256` permite auditar la identidad de esas siete copias. Los archivos originales se preservaron byte por byte.

## Entradas y supuestos

`datos_viga.csv` utiliza coma como separador y punto decimal. Sus columnas son `carga_kN` y `deflexion_medida_mm`. Contiene nueve observaciones (filas 2–10), de 0 a 40 kN, sin valores omitidos. Las deflexiones están entre 0 y 2,05 mm. No se suavizan, corrigen ni reemplazan los datos.

En `parametros_viga.xlsx`, hoja `Parametros`, B4:B7 contiene L = 4 m, b = 0,20 m, h = 0,40 m y E = 25 GPa. Se toma h en la dirección de la flexión. Se consideran sección y módulo constantes, carga estática centrada, apoyos ideales y pequeñas deformaciones. La deflexión se expresa como magnitud positiva. Se analiza el incremento debido a P; no se agrega peso propio, pues no se dispone de densidad. Se omiten cortante y efectos no lineales. No se identifica un material real a partir del valor de E.

### Fórmulas y conversiones

| Ubicación en `Analisis` | Fórmula guardada / operación | Unidad |
|---|---|---|
| D15 | `=B15*10^9` | E en N/m², a partir de GPa |
| D17 | `=D13*D14^3/12` | I en m⁴ |
| C24:C32 | `=B24*1000`, copiada hacia abajo | P en N, a partir de kN |
| E24:E32 | `=C24*$D$12^3/(48*$D$15*$D$17)`, copiada | Deflexión teórica en m |
| F24:F32 | `=E24*1000`, copiada | Deflexión teórica en mm |
| G24:G32 | `=D24-F24`, copiada | Diferencia con signo en mm |
| H24:H32 | `=ABS(G24)`, copiada | Diferencia absoluta en mm |
| I24:I32 | `=IF(B24=0,"n.a.",H24/ABS(F24))`, copiada | Cociente mostrado en formato porcentaje |
| J24:K32 | Deflexión medida/P y teórica/P, para P distinto de cero | mm/kN |

La diferencia relativa usa la deflexión **teórica** como denominador. No se multiplica por 100 dentro de I24:I32 porque el formato porcentaje ya lo hace al mostrarla. La fila P = 0 conserva sus deflexiones y diferencias absolutas; muestra `n.a.` para los cocientes no definidos y se excluye del promedio relativo. Los cálculos conservan su precisión y solo se redondea la presentación.

### Resultados de referencia

| Resultado | Valor |
|---|---:|
| I | 0,001066666667 m⁴ |
| Flexibilidad teórica δ/P | 0,05000 mm/kN |
| Deflexión teórica a 40 kN | 2,00 mm |
| Deflexión medida a 40 kN | 2,05 mm |
| Diferencia absoluta máxima | 0,05 mm |
| Diferencia relativa máxima | 4,00 % (a 5 kN) |
| Media de las ocho diferencias relativas | 1,880357 % |
| δmed/P para P > 0 | 0,05000–0,05200 mm/kN |

Las tres verificaciones documentadas son consistencia dimensional, cálculo independiente de 40 kN en N y mm y constancia aproximada de δ/P. El cálculo independiente convierte E a 25 000 N/mm² y da nuevamente 2,00 mm. Durante la preparación también se duplicó E en una copia temporal: la deflexión se redujo a la mitad y se restauró E = 25 GPa antes de guardar.

## Figura y actualización de salidas

El gráfico editable de Excel utiliza X = `Analisis!B24:B32` (kN), Y medida = `D24:D32` y Y teórica = `F24:F32` (mm). Incluye las nueve cargas de cada serie. 

La figura del reporte se preparó con PGFPlots a partir de `analysis/datos_figura.csv`. Sus columnas proceden, en orden, de B24:B32, D24:D32, F24:F32, G24:G32 e I24:I32 multiplicada por 100. El último campo queda vacío a carga cero. El origen se conserva aunque ambos puntos coincidan.

Para actualizar ese CSV sin programación, copie esos resultados **como valores** en una hoja temporal, mantenga los cinco encabezados existentes y guarde como CSV con coma separadora y punto decimal. Compruebe la primera y última fila y que se mantengan nueve registros. El CSV es una exportación estática: no se actualiza al guardar Excel.

Para reproducir el estilo publicado, compile `report/figura.tex` con pdfLaTeX conservando la ruta al CSV. Se obtiene una figura PDF; la imagen entregada corresponde a su conversión a PNG a 300 ppp. Alternativamente, exporte el gráfico de Excel a `figures/carga_deflexion.png`; los datos y unidades deben ser los mismos, aunque cambie el estilo. La tabla y las cifras redactadas de `main.tex` son estáticas y también deben actualizarse si cambian las entradas.

## Compilar la nota en Overleaf

No se recibió la plantilla Overleaf ni el BibTeX inicial mencionados en la consigna. Se elaboró una fuente independiente con todas las secciones requeridas. Si existe una plantilla obligatoria adicional en Moodle, traslade a ella este contenido.

## Herramientas y alcance de la verificación

La continuación prevista utiliza el explorador de archivos, Excel, GitHub web y el editor de Overleaf; no requiere Python, macros ni scripts de análisis. En el explorador conviene mostrar las extensiones para distinguir `.csv`, `.xlsx`, `.tex`, `.bib`, `.png` y `.pdf`.

Se comprobaron las entradas, fórmulas, resultados, visualizaciones y compilación local. No se ha ejecutado esta versión en una sesión de Microsoft Excel o de Overleaf del estudiante. Antes de entregar, abra la planilla en Excel, recompile en Overleaf y registre cualquier ajuste real. El detalle está en `docs/REVISION.md`.

## Interpretación y límites

Los datos presentan una tendencia aproximadamente lineal y diferencias pequeñas respecto del modelo en el rango proporcionado. La diferencia relativa máxima de 4 % es descriptiva: no constituye un criterio normativo de aceptación. No hay repeticiones ni incertidumbres para estimar significancia o causas físicas. La relación L/h = 10 hace pertinente revisar el cortante en un estudio más detallado; faltan propiedades para cuantificarlo. No se infiere resistencia, fisuración, capacidad última ni seguridad de una viga real.




