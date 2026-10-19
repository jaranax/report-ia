---
name: publicar-report-ia
description: Use cuando un informe nuevo de Report IA ya está añadido a informes/index.html y haya que revisarlo y subirlo al repositorio GitHub configurado.
---

# Publicar informes de Report IA

Prepara y publica en GitHub la página compartida de informes después de añadir o actualizar un informe. La skill `report-ia` redacta y actualiza el HTML; esta skill revisa el cambio, registra `informes/index.html` y cualquier ilustración nueva necesaria en `informes/images/` en la rama `main`, y comprueba que la integración Git de Cloudflare Pages publique automáticamente el commit.

## Configuración inicial, una sola vez

Configuración ya comprobada para este proyecto:

- Repositorio público de GitHub: `jaranax/report-ia`, rama `main`.
- Proyecto Cloudflare Pages: `report-ia`, conectado a `jaranax/report-ia`; despliegues automáticos habilitados para `main`.
- Configuración de compilación: `mkdir -p dist && cp informes/index.html dist/index.html`, salida `dist`.
- La conexión Git de Pages ya generó y publicó automáticamente el commit `b82fca09350d410caa996662c91946779b702d6c`. No hace falta crear otro proyecto ni configurar Wrangler.

## En cada informe

1. Comprueba que el conector de GitHub está activo para la cuenta autorizada y que existe el repositorio público `report-ia` con rama `main`. Si falta autenticación, pide completar el inicio de sesión una sola vez. Si el repositorio o la rama no coinciden, detente e informa del hallazgo.
2. Abre `informes/index.html` en el navegador y comprueba que se ve el informe recién añadido, que siguen apareciendo los informes anteriores y que los filtros de categoría funcionan. Si no puedes comprobarlo o encuentras un fallo, detente antes de publicar e informa del resultado.
3. Comprueba en el repositorio remoto el contenido actual de `informes/index.html` y de cada ilustración referenciada. Confirma que el archivo local incluye el informe nuevo, conserva los informes anteriores, que toda imagen referenciada existe y que no contiene información privada. No modifiques archivos ajenos al cambio solicitado.
4. Si el contenido no cambia respecto al repositorio, no crees un commit. Si está correcto, actualiza `informes/index.html` y añade las ilustraciones nuevas necesarias mediante el conector de GitHub. Para una ilustración binaria usa blobs codificados en base64 y crea un único commit que preserve el árbol remoto vigente. No uses escrituras forzadas ni borres historial. Confirma el SHA del commit.
5. Espera al flujo automático de Pages iniciado por el commit. No ejecutes Wrangler ni crees una implementación manual para el mismo cambio. La configuración de compilación copia el HTML a `dist/index.html`; no prepares otro directorio temporal.
6. Comprueba en Cloudflare Pages que hay una implementación de producción para `main` asociada al SHA recién creado. Si el estado está en curso, espera antes de concluir. Si la API de Cloudflare da un error de autenticación, usa el panel de Cloudflare si hay una sesión ya iniciada.
7. Abre `https://report-ia.pages.dev/` y confirma que muestra el informe actualizado. Si solo funciona la URL única del despliegue o la publicación falla, indica cuál comprobación pasó y el error concreto; no inicies una segunda publicación por Wrangler.

## Límites

- La persona usuaria autorizó de forma permanente los cambios normales necesarios en cualquier archivo de este proyecto y su actualización en el repositorio público `jaranax/report-ia`, rama `main`. Realiza los commits y pushes del trabajo solicitado sin pedir confirmación por cada archivo o actualización.
- Esta autorización cubre las actualizaciones rutinarias del contenido, las imágenes necesarias, los informes, las skills y las funciones del proyecto. Mantén cada commit acotado al trabajo solicitado y no incluyas secretos, credenciales ni datos privados.
- La autorización no incluye borrar o hacer privado/público el repositorio, cambiar dominios o ajustes de cuenta, modificar la configuración de GitHub o Cloudflare, ni asumir gastos. Para esas acciones, pregunta antes.
- La autorización para configurar inicialmente el repositorio público `report-ia` en GitHub y el proyecto Pages `report-ia` en Cloudflare se concedió en esta conversación. No crees otros repositorios o proyectos.
- No uses Wrangler para Report IA mientras la conexión Git y los despliegues automáticos estén habilitados. Si esa configuración cambia, verifica el nuevo método antes de publicar y actualiza esta skill.
- La autenticación inicial o renovación de las conexiones de GitHub y Cloudflare puede requerir que la persona usuaria complete un paso de inicio de sesión. Eso es un requisito técnico de acceso, no una aprobación para cada actualización.
- Cloudflare Pages publica automáticamente al recibir cambios en `main`. La configuración actual vigila `*`, por lo que otros cambios del repositorio también pueden iniciar una compilación; la web solo cambia si esos cambios alteran los archivos copiados al directorio `dist`.
- Si el repositorio, rama o contenido remoto muestran una situación distinta de la esperada, detente y describe el hallazgo; no adivines cómo resolverlo.
- Subir a GitHub no confirma por sí solo que Cloudflare haya terminado de publicar la página. Si Cloudflare Pages está conectado al repositorio, puede iniciar una publicación tras el push; comunica ese resultado solo si se ha comprobado.
