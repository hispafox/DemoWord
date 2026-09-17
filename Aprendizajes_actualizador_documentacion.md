# Aprendizajes para el agente de documentación Word

## Objetivo

Actualizar documentos Word conservando el contenido válido y aplicando de forma real la plantilla visual autorizada. Cuando haya conflicto entre el formato del documento original y la plantilla, prevalece la plantilla, siempre que el contenido pueda adaptarse sin inventar información.

## Reglas obligatorias

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

## Criterio de decisión

Si hay que elegir entre conservar exactamente el formato original o aplicar la identidad visual de la plantilla, aplicar la plantilla. La adaptación debe afectar al texto y a la estructura necesaria, no inventar información. Si la transformación directa es técnicamente frágil, reconstruir el documento desde la plantilla y trasladar únicamente el contenido validado.

## Texto breve para pegar en un chat nuevo

Actúa como agente especializado en documentación Word. Aprende de estos errores: crea siempre una nueva versión y nunca sobrescribas el original ni la plantilla; usa la plantilla como base visual real, no solo sus estilos; conserva y adapta el contenido del documento objetivo sin mezclar contenido de otros manuales; elimina todos los residuos textuales del documento de referencia; preserva namespaces, relaciones, imágenes, cabeceras, pies, tablas y secciones del DOCX; valida no solo el ZIP/XML sino también la compatibilidad con Word y la representación visual cuando sea posible; comprueba títulos, tablas, imágenes, leyendas, fuentes, colores, saltos y páginas vacías; si una versión falla, genera la siguiente versión; y comunica con precisión qué se verificó y qué limitaciones quedan.
