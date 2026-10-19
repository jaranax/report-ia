# Report IA

Proyecto de práctica con skills de Codex para revisar blogs sobre inteligencia artificial, resumir noticias y mantener informes temáticos en una página HTML compartida.

## Página publicada

[https://report-ia.pages.dev/](https://report-ia.pages.dev/)

## Qué ofrece

- **Informes:** reúnen noticias relacionadas con un tema, explican cada una en lenguaje sencillo y presentan una conclusión común. Se ordenan por última actualización y se pueden filtrar por categoría.
- **Noticias:** muestra cada resumen por separado, de la más reciente a la más antigua, con imagen, categoría, enlace a la fuente y al informe relacionado. Esta vista se genera a partir de las noticias de los informes; no mantiene una copia independiente de cada resumen. Usa la imagen de portada del artículo original cuando está disponible y una ilustración editorial generada cuando no la hay.
- **Diseño:** incluye una portada breve, navegación entre las vistas y una nota sobre el uso de las fuentes.

## Skills del proyecto

- `.agents/skills/report-ia/`: revisa uno o varios blogs sobre el tema indicado y añade noticias relevantes a `informes/index.html`. Mantiene un informe acumulativo por tema, evita duplicados y actualiza la conclusión.
- `.agents/skills/publicar-report-ia/`: revisa el cambio, sube `informes/index.html` a la rama `main` de GitHub y comprueba que Cloudflare Pages publique automáticamente la actualización.

## Archivos y publicación

- `informes/index.html` es la página que se publica. Las ilustraciones generadas se guardan en `informes/images/` y se sirven desde el repositorio público; las imágenes originales enlazadas se cargan desde la fuente.
- Los archivos `informes/AAAA-MM-DD-*.html` son instantáneas de revisiones anteriores que se conservan en GitHub. La compilación de Cloudflare copia solo `informes/index.html` a `dist/index.html`.
- `blogs-por-revisar.md` guarda blogs candidatos para evaluar si encajan en el proyecto.
- El repositorio es `jaranax/report-ia`, rama `main`. Cloudflare Pages está conectado a esa rama y publica sus cambios automáticamente.
- `.wrangler/`, `node_modules/` y los archivos de entorno o credenciales están excluidos del repositorio.
