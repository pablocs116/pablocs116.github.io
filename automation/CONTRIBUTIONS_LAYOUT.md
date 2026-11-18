# Rediseño de "Open Source Contributions" cuando crezca

Documento permanente (no se regenera como CLAUDE_CODE_TASKS.md). La tarea automática debe leerlo en cada ejecución, antes de añadir contribuciones nuevas.

## Estado actual (2026-11-13)
Diseño v1: un grupo por repo (`contributionGroups` en el template de `index.html`) con cabecera `owner/name`, contador ("N merged PRs"), una línea de resumen del repo y todas las PRs listadas debajo, de la más reciente a la más antigua. Sin colapsar nada.
Inventario (2026-11-18): 2 repos, 8 PRs (TransformerLens 5, SAELens 3), más 2 menores mostradas como contador en la cabecera (TransformerLens +1 test fix, SAELens +1 test config).

## Paso 0 — ¿Contribución mayor o menor?
Las filas de la sección sirven para que quien lea vea, en una frase, **qué aportó Pablo a la librería**. Antes de añadir una PR mergeada, clasifícala con esta pregunta:

> ¿Se puede explicar en una frase qué puede hacer ahora un usuario de la librería, o qué deja de fallarle, gracias a esta PR, y a un lector le interesaría?

- **Sí → mayor** (`known_contributions`): fila completa con su resumen. Ejemplos: adapters de arquitectura (TransformerLens #1478, #1483, #1994), cargar modelos en formato antiguo de TransformerLens con TransformerBridge (SAELens #789).
- **No → menor** (`minor_contributions`, con `type`): no lleva fila. Ejemplos: arreglos o configuración de tests (TransformerLens #1998, SAELens #788), cambios de CI o de docs, fixes de una línea sin efecto visible para el usuario.

El tamaño (+líneas) no decide: una PR pequeña que arregla un fallo real puede ser mayor, y una grande que solo reorganiza tests es menor. Si dudas, márcala como menor y pon la duda en CLAUDE_CODE_TASKS.md, en "Requiere aprobación".

## Contribuciones menores como métrica, por repo
Las menores no se listan una a una, pero **cuentan en su repo**, para que se vea en qué librerías ha contribuido más Pablo:
- En la cabecera de cada grupo, junto al contador de PRs, se añade el número de menores de ese repo, por ejemplo "3 merged PRs · +2 smaller (tests, config)". Los tipos salen del `type` de `minor_contributions` de ese repo, sin enlaces.
- Se muestra desde la primera menor. Un repo sin menores se queda como está.
- Un repo con menores pero sin ninguna mayor tiene un grupo de una sola línea: la cabecera `owner/name` y el contador ("+2 smaller contributions (tests)"), sin resumen ni filas. Cuenta como repo para el umbral 2 del paso 1.
- Se actualiza en cada ejecución. No es un rediseño y no necesita aprobación.

## Paso 1 — Cuándo hace falta un diseño nuevo
Antes de añadir una entrada, cuenta lo que habría en la sección **después** de añadirla (fuente: `known_contributions` con status "applied" o "queued" en `state.json`). Si se cumple **cualquiera** de estos umbrales, el diseño v1 ya no vale:

1. **Un repo con más de 5 PRs.** El grupo deja de leerse de un vistazo.
2. **4 o más repos**, o **más de 12 PRs en total.** La sección pasa de ~2 pantallas de móvil (375 px) y entierra las secciones de abajo.
3. **Pablo lo pide**, o una PR nueva no cabe bien en ninguna fila ni grupo existente (por ejemplo, una contribución que no es PR: issue, release, mantenimiento).

Si salta un umbral:
- **Añade igualmente la entrada aprobada** con el diseño v1 (no bloquees contenido aprobado).
- **No rediseñes por tu cuenta.** En CLAUDE_CODE_TASKS.md, en una sección "Requiere aprobación", escribe qué umbral ha saltado, con los números, y la propuesta del paso 2.
- No vuelvas a proponerlo en cada ejecución: anótalo en `state.json` como `"layout_review": {"triggered": "<fecha>", "reason": "...", "status": "proposed"}` y solo actualízalo si cambia el motivo.

## Paso 2 — Cómo diseñar la nueva organización
1. **Inventario.** Lista todas las contribuciones por repo, con fecha, tamaño (+líneas) y tema (adapter de arquitectura, migración a TL4, fix de tests…). El tema dice si conviene agrupar por repo o por línea de trabajo.
2. **Elige la opción más pequeña que resuelva el umbral que ha saltado**, en este orden:
   - **A. Colapsar dentro del grupo** (umbral 1): mostrar las 3 PRs más recientes y un botón "Show N more" que despliega el resto. El resumen del repo y el contador se quedan como están. Es el cambio más pequeño.
   - **B. Grupos compactos** (umbral 2): cada repo se muestra cerrado (cabecera, contador, resumen y la PR más destacada) y se abre al tocarlo. Encima, una línea de totales ("N merged PRs across M repos").
   - **C. Destacadas + resto** (umbral 2 con muchos repos): 3–4 PRs destacadas (las de más impacto, elegidas con Pablo) como tarjetas completas, y debajo una lista compacta de una línea por PR, agrupada por repo.
   Las opciones se pueden combinar (por ejemplo, A + B).
3. **Restricciones fijas.**
   - Se mantiene el tema terminal/interpretability.
   - Cada PR conserva su enlace.
   - Orden cronológico inverso dentro de cada grupo.
   - Los nombres largos tienen que partirse bien en móvil: `<wbr>` tras la barra en `owner/name` y `overflow-wrap:anywhere` en títulos (commits 9712887 y 5dae1df).
   - Nada de dependencias externas nuevas: el cambio va en el template y los datos del bundle de `index.html`.
   - Con JS desactivado, o antes de que cargue, el contenido sigue estando disponible.
4. **Prototipo y comprobación.** Implementa en una rama, renderiza en local a 375 px y en escritorio (Chrome headless con `--dump-dom` o abriendo `index.html`) y comprueba que no hay scroll horizontal y que la sección mide menos de ~2 pantallas de móvil.
5. **Aprobación.** Describe la opción elegida, el motivo y el antes/después de longitud (capturas si es posible) en "Requiere aprobación". No se fusiona hasta que Pablo lo apruebe.
6. **Después de fusionar.** Actualiza "Estado actual" en este documento (v2, qué opción, inventario), pon `layout_review.status` a `"applied"` y ajusta los umbrales del paso 1 al nuevo diseño. Por ejemplo, con la opción A el umbral 1 pasa a ser "más de 12 PRs en un repo".
