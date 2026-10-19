---
name: report-ia
description: Revisa uno o varios blogs sobre un tema indicado y crea un informe HTML breve que explica las noticias en lenguaje sencillo. Úsala cuando se proporcione un blog y un tema para revisar.
---

# Informe de noticias de un blog

Revisa noticias de uno o varios blogs sobre el tema que indique la persona usuaria y añade un informe por encargo a una página HTML compartida. Cada informe reúne varias noticias relacionadas, las resume en lenguaje sencillo y termina con una conclusión común destacada. Los blogs y el tema son variables de cada encargo; no asumas que siempre son Xataka o The Batch.

## Datos de entrada

- Blog o blogs: URL indicada por la persona usuaria.
- Tema: asunto elegido para filtrar las noticias.
- Periodo por defecto: últimos 30 días, contado desde la fecha de revisión.
- Límite por defecto: hasta 3 artículos relevantes por blog.
- Idioma del informe por defecto: español.

Si falta la URL del blog o el tema y no se pueden inferir con claridad del encargo, pregunta solo por el dato que falte. La persona usuaria puede cambiar el periodo, el límite o el idioma.

## Pasos

1. Abre cada blog indicado en el navegador. Revisa su índice, archivo, buscador o sección temática para localizar artículos del periodo solicitado.
2. Selecciona hasta el límite indicado por blog que traten directamente el tema. Comprueba la fecha y abre cada artículo seleccionado para leer suficiente contenido para resumirlo. No elijas un artículo solo por coincidir una palabra del título.
3. Crea o actualiza informes/index.html. Mantén un informe acumulativo por tema: si ya existe uno sobre el mismo tema, añade las noticias nuevas que cumplan los criterios, sin duplicar artículos, y actualiza su resumen, conclusión, periodo cubierto y fecha de última actualización. No crees un informe separado por cada noticia ni por cada nueva revisión del mismo tema. Si el tema es distinto, crea otro informe. Ordena los informes por fecha de última actualización, de más reciente a más antigua.
4. Asigna a cada informe una o varias categorías temáticas breves. Reutiliza categorías existentes cuando encajen y añade un filtro visible para mostrar todos los informes o filtrar por categoría. El filtro debe funcionar en la propia página, sin servicios externos.
5. Para cada noticia, añade a su sección de origen los datos `data-category`, `data-image` y `data-image-alt`. La vista Noticias los usa para mostrar una tarjeta con imagen a la izquierda y categoría, título y resumen a la derecha. La categoría describe la noticia; reutiliza una categoría existente cuando encaje. No hagas que toda la tarjeta sea un enlace o desplegable.

## Contenido del informe

- Título y fecha de última actualización, periodo cubierto y blogs consultados.
- Una sección por noticia con título enlazado al original, blog, fecha y explicación breve en términos cotidianos.
- Una conclusión general, breve y visualmente destacada, que conecte las noticias y esté respaldada por ellas. Si las noticias no permiten sostener una conclusión común, indícalo claramente y no fuerces una.
- Categorías del informe y un control para filtrar por categoría.
- Imagen en la tarjeta individual de cada noticia: primero busca la imagen principal o `og:image` del artículo original y enlázala directamente; escribe un texto alternativo descriptivo. Si no hay una imagen editorial apropiada, genera una ilustración conceptual, guárdala en `informes/images/` y apunta a ella mediante `https://raw.githubusercontent.com/jaranax/report-ia/main/informes/images/<archivo>`, porque la compilación de Pages copia solo `informes/index.html`. Márcala como ilustración en su texto alternativo y no la presentes como fotografía del hecho. Si una imagen no carga, deja la tarjeta legible y muestra el estado de imagen no disponible.
- Diseño legible en móvil y escritorio, con CSS y el comportamiento del filtro incluidos en el mismo HTML.

Si informes/index.html aún no existe, créala con el primer informe. Si ya existe, lee su estructura: actualiza el informe del mismo tema o añade uno nuevo si el tema es distinto. Conserva las noticias anteriores y los demás informes. Si hay informes previos como archivos HTML independientes, incorpóralos a la página compartida cuando su contenido esté disponible y sea verificable; conserva esos archivos originales.

Atribuye a cada blog sus afirmaciones y separa los hechos que el artículo reporta de la opinión editorial y de las conclusiones de síntesis. No inventes fechas, detalles, resultados ni contexto. Si no puedes abrir o verificar un artículo, exclúyelo o indica claramente la limitación; no rellenes los huecos. Si no encuentras artículos suficientes, informa cuántos encontraste en vez de completar el cupo con noticias poco relacionadas.

Esta skill mantiene la página para revisión local. No la publica, no la envía y no hace cambios en GitHub; esas acciones pertenecen a un flujo separado.
