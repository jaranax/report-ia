---
name: publicar-report-ia
description: Use cuando un informe nuevo de Report IA ya está añadido a informes/index.html y haya que revisarlo y subirlo al repositorio GitHub configurado.
---

# Publicar informes de Report IA

Prepara y publica en GitHub y Cloudflare Pages la página compartida de informes después de añadir un informe. La skill `report-ia` redacta y actualiza el HTML; esta skill verifica ese cambio, lo registra en GitHub mediante el conector disponible y publica la página con Wrangler. No requiere un repositorio Git local.

## Configuración inicial, una sola vez

La persona usuaria autorizó crear un repositorio público de GitHub llamado `report-ia` y un proyecto Cloudflare Pages llamado `report-ia`, además de usar Wrangler. Completa esta preparación cuando estén disponibles las conexiones de cuenta:

1. Comprueba que la raíz del proyecto es la carpeta correcta y que no hay archivos secretos o privados que deban excluirse del repositorio público. No publiques credenciales, tokens, archivos de configuración local ni datos personales.
2. Crea el repositorio público `report-ia` en la cuenta GitHub autorizada, si todavía no existe. La configuración inicial sube el proyecto, sus skills y los informes existentes a la rama `main`. Excluye `.wrangler/`, credenciales, tokens, archivos `.env` y cachés locales.
3. Crea el proyecto Pages `report-ia` en Cloudflare, si todavía no existe. La cuenta ya puede autenticarse mediante Wrangler. En la versión comprobada `4.151.1`, el comando de creación directo que funcionó fue `npx --yes wrangler@4.151.1 pages project create report-ia --production-branch main --force`. Usa `--force` solo para esta creación inicial cuando Wrangler muestre el aviso que redirige la creación de Pages al flujo de Workers; no lo uses en despliegues posteriores.
4. Completa una vez la autenticación inicial de GitHub y Cloudflare si la herramienta la solicita. No solicites una autorización nueva para cada informe.

Si no puedes completar una conexión de cuenta, indica qué inicio de sesión falta y conserva el resto de la preparación ya realizada.

## En cada informe

1. Comprueba que el conector de GitHub está activo para la cuenta autorizada y que existe el repositorio público `report-ia` con rama `main`. Si falta autenticación, pide completar el inicio de sesión una sola vez. Si el repositorio o la rama no coinciden, detente e informa del hallazgo.
2. Abre `informes/index.html` en el navegador y comprueba que se ve el informe recién añadido, que siguen apareciendo los informes anteriores y que los filtros de categoría funcionan. Si no puedes comprobarlo o encuentras un fallo, detente antes de publicar e informa del resultado.
3. Comprueba en el repositorio remoto el contenido actual de `informes/index.html`. Confirma que el archivo local incluye el informe nuevo, conserva los informes anteriores y no contiene información privada. No modifiques archivos ajenos a este informe.
4. Si el contenido local no cambia respecto al del repositorio, no crees un commit. Si está correcto, actualiza únicamente `informes/index.html` mediante el conector de GitHub, usando su SHA actual y un mensaje breve. No uses escrituras forzadas ni borres historial. Confirma el SHA del commit.
5. Prepara un directorio temporal que contenga únicamente `informes/index.html`, con el nombre `index.html`. Así los informes antiguos independientes no se publican como páginas separadas.
6. Despliega con `npx --yes wrangler@4.151.1 pages deploy <directorio-temporal> --project-name report-ia --branch main`. Si Wrangler no está disponible, usa `npx`; no añadas Wrangler como dependencia del proyecto. No uses `--force` al desplegar. Si pide iniciar sesión, completa la renovación técnica de acceso sin pedir aprobación para publicar.
7. Comprueba que el despliegue terminó correctamente y que `https://report-ia.pages.dev/` responde con HTTP 200 y muestra el informe actualizado. Comunica el commit de GitHub y la URL publicada. Si Cloudflare falla tras el push, deja constancia de que GitHub sí se actualizó y explica el error exacto de Cloudflare.

## Límites

- La autorización de la persona usuaria para publicar Report IA es permanente para futuras actualizaciones del proyecto. Después de cada informe nuevo o actualizado, realiza la revisión, el commit y el push de `informes/index.html` y despliega la página en Cloudflare Pages, siempre que las comprobaciones de este flujo pasen. No vuelvas a pedir aprobación para cada publicación.
- La autorización permanente cubre únicamente la página de informes y su despliegue. No cubre cambios a otros archivos, gastos, cambios de dominio, cambios de visibilidad del repositorio ni cambios de configuración de GitHub o Cloudflare.
- La autorización para configurar inicialmente el repositorio público `report-ia` en GitHub y el proyecto Pages `report-ia` en Cloudflare se concedió en esta conversación. No crees otros repositorios o proyectos.
- Para este proyecto, la autorización explícita de Wrangler en esta conversación sustituye el método de publicación indicado por la skill global de Cloudflare Pages. Mantén esta excepción limitada a Report IA.
- La autenticación inicial o renovación de las conexiones de GitHub y Cloudflare puede requerir que la persona usuaria complete un paso de inicio de sesión. Eso es un requisito técnico de acceso, no una aprobación para cada actualización.
- La autorización permanente permite revisar, hacer commit, subir a GitHub y desplegar `informes/index.html` en cada informe. No cubre cambios de dominio, gastos, visibilidad del repositorio ni cambios de configuración que no estén descritos arriba.
- Si el repositorio, rama o contenido remoto muestran una situación distinta de la esperada, detente y describe el hallazgo; no adivines cómo resolverlo.
- Subir a GitHub no confirma por sí solo que Cloudflare haya terminado de publicar la página. Si Cloudflare Pages está conectado al repositorio, puede iniciar una publicación tras el push; comunica ese resultado solo si se ha comprobado.

