# Encargo para Claude Code — pablocs116.github.io
Generado: 2026-11-13

## Contexto
`index.html` es un bundle empaquetado (ver <script type="__bundler/manifest"> y <script type="__bundler/template">). Antes de tocar nada, revisa los commits ee203db y 9712887 (agrupación de "Open Source Contributions" por repo) y el commit "Add SAELens #785 to Open Source Contributions" del 2026-11-12 como ejemplo de cómo se añadió una entrada anteriormente. Prueba localmente (abre index.html o corre Jekyll) antes de hacer push.

## Aplicar directo (Pablo lo aprobó el 2026-11-13)
TODO 1. En la sección "Open Source Contributions", dentro del grupo SAELens (decoderesearch/SAELens), añadir una fila junto a #784 y #785 (estas dos YA están en el sitio, no duplicarlas): #789 "fix: load old TransformerLens-format models with TransformerBridge" (compatibilidad al cargar modelos en el formato antiguo de TransformerLens con TransformerBridge). Link: https://github.com/decoderesearch/SAELens/pull/789. NUEVA. Mantener el formato de las filas existentes y el ajuste móvil de nombres largos.

TODO 2. Como SAELens ya tendrá tres PRs (#784, #785, #789), mostrar el grupo con una línea corta de resumen del repo (por ejemplo compatibilidad de SAELens con TransformerLens 4 / TransformerBridge) y las PRs listadas debajo. Pablo aprobó esta reorganización el 2026-11-13; si el diseño actual ya lo permite, no cambiar nada más.

## No añadir todavía
TransformerLens #1998 (arreglo de un test float32) y SAELens #788 (config de tests): contribuciones menores, guardadas en state.json bajo "minor_contributions".
pyvene #242 (gradient checkpointing): abierta, sin mergear.
Forks (TransformerLens, pyvene, SAELens): no se listan.
chemical-J-spaces: rechazado por Pablo, no incluir nunca.

## Al terminar
Actualiza `automation/state.json` marcando "applied" SAELens #789.
