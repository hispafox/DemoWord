# Aprendizajes para el agente de documentación Word

## Objetivo

Actualizar documentos Word conservando el contenido válido y aplicando de forma real la plantilla visual autorizada. Cuando haya conflicto entre el formato del documento original y la plantilla, prevalece la plantilla, siempre que el contenido pueda adaptarse sin inventar información.

## Reglas obligatorias

### Regla de arranque

Este archivo es un registro histórico para mantenimiento humano; no es una fuente que el agente deba consultar durante una actualización. El agente debe aplicar las reglas incorporadas en su propio `.agent.md`, usando únicamente el documento objetivo y `Plantilla.docx` y `Manual Usuario Nuevo.docx` como referencias documentales autorizadas. Antes de generar una versión debe elaborar una matriz de aceptación: contenido conservado, estructura, geometría, escala tipográfica, fuentes, anchos de tabla, secciones, recursos usados, densidad por página y evidencia visual necesaria.

1. **Crear siempre una nueva versión**
   - Nunca sobrescribir el documento original.
   - Nunca modificar `Plantilla.docx` ni las referencias visuales.
   - Usar nombres versionados consecutivos, por ejemplo `Documento_v2.docx`, `Documento_v3.docx`.
   - Mantener las versiones anteriores para poder comparar y recuperar.

2. **Usar la plantilla como base real**
   - No basta con copiar estilos de párrafo ni con validar que existan `styles.xml`, tablas o cabeceras.
   - Cuando se indique aplicar el estilo de una plantilla, construir el nuevo documento a partir del paquete de la plantilla o reproducir fielmente su estructura.
   - Conservar, cuando sean aplicables, tamaño de página, márgenes, tipografías, colores, cabeceras, pies, numeración, tablas, espaciados, saltos de sección y composición de capítulos.
   - No sustituir el contenido del documento objetivo por el contenido de otro manual solo porque ese otro documento tiene el estilo deseado.

3. **Conservar y adaptar el contenido**
   - Leer primero el contenido completo del documento objetivo.
   - Reutilizar sus textos, tablas e imágenes cuando sean pertinentes.
   - Adaptar títulos, introducciones, leyendas y textos para encajar en la estructura de la plantilla.
   - No inventar datos, pantallas, cifras, pasos, requisitos ni resultados.
   - Eliminar cualquier resto de contenido de otro documento: títulos, leyendas, cabeceras, tablas, términos y referencias cruzadas.
   - Hacer una búsqueda final de términos propios del documento de referencia que no pertenezcan al documento objetivo.

4. **Editar DOCX sin romper Word**
   - Un DOCX es un paquete ZIP con relaciones y XML interdependientes.
   - No considerar suficiente que `document.xml` sea parseable.
   - Evitar reserializar XML con una herramienta que cambie o pierda declaraciones de espacios de nombres.
   - Preservar los prefijos y atributos de compatibilidad, especialmente `mc:Ignorable` y sus namespaces (`w14`, `wp14`, etc.).
   - Si se sustituyen imágenes, actualizar simultáneamente `word/media/`, `word/_rels/document.xml.rels` y las referencias `r:embed`.
   - Conservar las relaciones de headers, footers, numbering, estilos, tema y recursos.
   - Mantener las leyendas inmediatamente junto a la figura y no insertar texto entre una imagen y su leyenda.

5. **Validar en varios niveles**
   - Validar el ZIP y todas las partes XML.
   - Comprobar que el documento tiene las tablas, imágenes, cabeceras, pies, estilos y secciones esperados.
   - Comprobar el texto visible completo, no solo los primeros párrafos.
   - Revisar que no queden términos del documento de referencia.
   - Renderizar o abrir con una herramienta compatible con Word cuando esté disponible. La validez del ZIP/XML no demuestra por sí sola que Word pueda abrir el documento sin reparación.
   - Revisar visualmente: página inicial, saltos, títulos huérfanos, tablas partidas, imágenes deformadas, leyendas, fuentes, colores y páginas vacías.
   - Si Word muestra “contenido no legible”, no dar por válida la entrega: revisar namespaces, relaciones, `sectPr`, estilos y reconstruir desde la plantilla.

6. **Trabajar de forma incremental**
   - Antes de editar, formular una hipótesis local sobre el problema y una comprobación que pueda refutarla.
   - Después de la primera edición, ejecutar una validación focalizada antes de seguir explorando o haciendo cambios adicionales.
   - Si una validación falla, corregir la misma versión en curso solo si todavía no se ha entregado; si ya existe una versión entregada, crear la siguiente versión.
   - Eliminar scripts temporales después de validar.

7. **Comunicar con precisión**
   - Indicar siempre la ruta exacta del nuevo archivo.
   - Resumir qué contenido se conservó, qué se adaptó y qué elementos de plantilla se aplicaron.
   - Separar claramente las comprobaciones realizadas de las comprobaciones no disponibles.
   - No afirmar que un documento “abre correctamente en Word” si solo se ha comprobado como ZIP/XML.
   - Si hay una limitación de validación visual, declararla expresamente.

## Procedimiento recomendado

1. Localizar el documento objetivo, la plantilla y las referencias autorizadas.
2. Leer el contenido y analizar estilos, tablas, imágenes, cabeceras, pies, relaciones y secciones.
3. Crear una nueva versión, sin modificar el original ni la plantilla.
4. Usar la plantilla como paquete base y adaptar dentro de ella el contenido del objetivo.
5. Revisar el texto visible para eliminar residuos del contenido de referencia.
6. Validar ZIP, XML, relaciones, estructura y recursos.
7. Renderizar o abrir con Word cuando sea posible y corregir los problemas visuales.
8. Eliminar auxiliares y entregar la ruta de la nueva versión.

## Aprendizajes de la comparación Mac vs PC

- No basta con copiar los estilos de la plantilla. `Title`, `Heading1` y `Heading2` pueden tener tamaños pensados para un manual y resultar desproporcionados en un informe corto. Medir y adaptar la escala antes de generar.
- La tabla debe calcularse con el ancho útil de la página: ancho de papel menos márgenes izquierdo y derecho. Si la suma de columnas lo supera, Word recorta o desborda el contenido.
- No usar saltos de sección para separar capítulos si no cambia la configuración de página, encabezado o pie. Un `sectPr` adicional puede crear una página vacía; mantener los saltos internos justificados y un único `sectPr` final.
- Un informe comparativo necesita una composición editorial propia: título contenido, resumen inicial, bloques de decisión y una tabla legible. Una sucesión de encabezados heredados de un manual produce páginas vacías y poca densidad informativa.
- La validación XML demuestra integridad técnica, no calidad visual. Renderizar antes de entregar y revisar la primera página, tablas, páginas vacías, fuentes, colores y saltos.
- Si no hay herramienta de renderizado, declararlo expresamente y no afirmar que el documento está visualmente validado. Una captura del usuario debe tratarse como evidencia de regresión y orientar una corrección causal.

## Auditoría de las cinco versiones del informe

- El original tenía una sola sección, una tabla y el contenido completo del informe.
- v2 trasladó el contenido a la plantilla, pero heredó tamaños de manual sin medirlos, definió una tabla de 8400 dxa cuando el ancho útil era 6520 dxa y añadió tres saltos de sección internos además del `sectPr` final. Resultado: títulos sobredimensionados, tabla recortada y página vacía.
- v3 solo redujo tamaños tipográficos. No reparó el ancho de tabla ni la estructura de secciones; demuestra que una corrección cosmética no sustituye al diagnóstico estructural.
- v4 corrigió el ancho de tabla a 6520 dxa y dejó dos saltos internos más un `sectPr` final. La reparación eliminó la causa de la página vacía.
- v5 añadió un resumen visual Mac/PC para dar densidad editorial y acercar el informe a la plantilla, conservando los conceptos del original y sin residuos del manual de referencia.
- Las cinco versiones conservaron los conceptos principales del original y no arrastraron términos de Nóvaris, vacaciones, solicitud y aprobación ni permisos y registro. Esta comprobación debe repetirse como comparación completa, no solo como búsqueda de frases.
- La secuencia de cinco versiones se produjo porque el agente validó primero la integridad XML y solo después reaccionó a capturas visuales. Regla: definir antes de generar la matriz de aceptación y no cerrar una tarea visual sin render o captura revisada.
- v2 y v5 conservaron ocho recursos multimedia de la plantilla aunque `document.xml` no referenciaba ninguna imagen. Regla: al construir desde un paquete base, limpiar medios y relaciones no utilizados, salvo que formen parte de cabeceras, pies o recursos requeridos.

## Criterio de decisión

Si hay que elegir entre conservar exactamente el formato original o aplicar la identidad visual de la plantilla, aplicar la plantilla. La adaptación debe afectar al texto y a la estructura necesaria, no inventar información. Si la transformación directa es técnicamente frágil, reconstruir el documento desde la plantilla y trasladar únicamente el contenido validado.

## Texto breve para pegar en un chat nuevo

Actúa como agente especializado en documentación Word. Lee primero `Aprendizajes_actualizador_documentacion.md`, la plantilla autorizada y el documento objetivo completo. Antes de editar, define una matriz de aceptación con contenido, estructura, geometría, escala tipográfica, fuentes, ancho útil de tablas, secciones, recursos y evidencia visual. Crea una única versión candidata, nunca sobrescribas el original ni la plantilla, y no uses v2-v5 como base de un documento nuevo. Usa la plantilla como base visual real, conserva y adapta el contenido sin mezclar manuales, elimina residuos, limpia recursos y relaciones no utilizados, preserva namespaces, relaciones, imágenes, cabeceras, pies, tablas y secciones, y compara el candidato con el original completo. No heredes tamaños de título sin medirlos, no superes el ancho útil de página y no uses saltos de sección para separar capítulos sin una razón real. Valida ZIP/XML, relaciones, contenido, geometría y paginación; renderiza o revisa una captura antes de cerrar. Si no hay evidencia visual, marca el archivo como candidato técnico y no como entrega final. Comunica con precisión qué se verificó y qué limitaciones quedan.
