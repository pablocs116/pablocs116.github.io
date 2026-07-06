# Encargo para Claude Code — Versión responsive/móvil de pablocs116.github.io

Generado: 2026-07-06 (a petición de Pablo, vía Cowork)

## Contexto
El sitio (index.html) es un archivo "bundle" empaquetado: contiene un <script type="__bundler/manifest"> con assets binarios (fuentes, librerías JS) en base64/gzip, y el contenido real de la página vive en <script type="__bundler/template">. NO se editó a mano por navegador porque es frágil — por eso este encargo es para ejecutarse localmente con Claude Code, con capacidad real de probar antes de publicar.

Revisa el commit d36baaf (https://github.com/pablocs116/pablocs116.github.io/commit/d36baaf) como ejemplo de una edición anterior a este mismo archivo.

También ten en cuenta que existe una tarea automática recurrente (automation/CLAUDE_CODE_TASKS.md y automation/state.json en este repo) que añade periódicamente entradas nuevas a las secciones "Repositorios" y "Open Source Contributions". El diseño responsive debe asumir que esas listas van a seguir creciendo con el tiempo.

## Decisiones ya tomadas por Pablo (no las cuestiones)
- Enfoque: responsive — mismo sitio, misma URL y contenido, se adapta con CSS según el tamaño de pantalla (no un build móvil separado).
- Estilo visual: mantener el mismo tema terminal/interpretability en todos los tamaños (misma identidad visual, no simplificar el look).

## Alcance del proyecto (decidido por Claude/Cowork, con justificación)
Se decidió el alcance más amplio de los propuestos — maquetación + simplificar contenido + rendimiento — por estas razones:

A. Maquetación es la base obligatoria: ajustar tipografía, espaciados y que las secciones se apilen bien en pantallas pequeñas (esto tenía que pasar sí o sí).
B. Simplificar contenido (colapsar secciones largas en acordeones/"mostrar más") es necesario porque las secciones "Repositorios" y "Open Source Contributions" se alimentan automáticamente y van a seguir creciendo — sin esto, en unos meses el móvil será un scroll interminable. Mejor resolverlo ahora que como parche después.
C. Rendimiento importa especialmente en móvil: el index.html actual empaqueta fuentes y librerías como base64 inline dentro del HTML (ver manifest), lo que infla el payload inicial. En redes móviles esto se nota mucho más que en desktop. Conviene resolverlo en la misma pasada ya que se está tocando el bundle de todas formas.

## Objetivos concretos
A. Layout totalmente responsive (breakpoints sugeridos: mayor o igual a 1200 desktop, ~768 tablet, ~390 móvil). Nada de overflow horizontal, texto legible sin zoom, targets táctiles de tamaño adecuado (mín. ~44px).
B. Adaptar (no eliminar) efectos que dependen de hover puro (ej. tooltips, reveals) a equivalentes táctiles (tap/focus) para que no quede contenido inalcanzable en móvil. Los layouts lado-a-lado que no quepan deben apilarse.
C. Colapsar en acordeones o "mostrar más" las secciones que crecen con el tiempo: Experiencia, Repositorios, Open Source Contributions. Mostrar por defecto un número razonable de entradas (ej. 3-5) y expandir el resto con un tap.
D. Optimizar peso inicial para móvil: evaluar font-display: swap, diferir JS no crítico, y si es viable sin romper el despliegue de archivo único, dividir/cachear los assets pesados en vez de inlinearlos todos. No sacrifiques la simplicidad de despliegue (GitHub Pages) si el trade-off no lo justifica — usa criterio.
E. NO cambies el contenido/copy existente (texto de experiencia, educación, bios) — este es un proyecto de layout/rendimiento, no una reescritura.

## Proceso sugerido
A. Antes de tocar nada: abre https://pablocs116.github.io en emulación de móvil (ej. iPhone 14, 390x844) en devtools y documenta los problemas actuales concretos (qué se rompe, qué es ilegible, qué queda inalcanzable) como línea base "antes".
B. Haz los cambios sobre una copia local, probando en los tres breakpoints antes de cada commit.
C. Verifica que el despliegue de GitHub Pages no falle tras el push (pestaña Actions).
D. Si cambias la estructura de secciones (ids, clases, marcado) de forma que afecte a cómo la tarea automática github-site-updater inserta nuevas entradas, actualiza automation/CLAUDE_CODE_TASKS.md con una nota indicando el nuevo patrón a seguir (en vez de referenciar el commit d36baaf, que quedaría desactualizado).

## Entregable
Un PR o commit directo a main (lo que Pablo prefiera) con el sitio responsive, más un resumen breve (puede ser el propio mensaje de commit o un comentario) de qué cambió y qué verificaste en cada breakpoint.
