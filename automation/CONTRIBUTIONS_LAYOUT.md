# Rediseño de "Open Source Contributions" cuando crezca

Documento permanente (no se regenera como CLAUDE_CODE_TASKS.md). La tarea automática debe leerlo en cada ejecución, antes de añadir contribuciones nuevas.

## Estado actual (2026-11-13)
Diseño v1: un grupo por repo (`contributionGroups` en el template de `index.html`) con cabecera `owner/name`, contador ("N merged PRs"), una línea de resumen del repo y todas las PRs listadas debajo, de la más reciente a la más antigua. Sin colapsar nada.
Inventario: 2 repos, 6 PRs (TransformerLens 3, SAELens 3).

## Paso 1 — Cuándo hace falta un diseño nuevo
Antes de añadir una entrada, cuenta lo que habría en la sección **después** de añadirla (fuente: `known_contributions` con status "applied" o "queued" en `state.json`). Si se cumple **cualquiera** de estos umbrales, el diseño v1 ya no vale:

1. **Un repo con más de 5 PRs.** El grupo deja de leerse de un vistazo.
2. **4 o más repos**, o **más de 12 PRs en total.** La sección pasa de ~2 pantallas de móvil (375 px) y entierra las secciones de abajo.
3. **5 o más contribuciones menores** en `minor_contributions` del mismo repo. Ya no tiene sentido ocultarlas, pero tampoco darles una fila completa a cada una.
4. **Pablo lo pide**, o una PR nueva no cabe bien en ninguna fila ni grupo existente (por ejemplo, una contribución que no es PR: issue, release, mantenimiento).

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
   - **D. Contribuciones menores** (umbral 3): una sola línea por repo, por ejemplo "+ 4 smaller fixes (tests, config)", con enlaces a las PRs. Nunca filas completas.
   Las opciones se pueden combinar (por ejemplo, A + D).
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
