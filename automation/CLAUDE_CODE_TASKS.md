# Encargo para Claude Code — pablocs116.github.io
Generado: 2026-11-10

## Contexto
`index.html` es un bundle empaquetado (ver <script type="__bundler/manifest"> y <script type="__bundler/template">). Antes de tocar nada, revisa el commit d36baaf (https://github.com/pablocs116/pablocs116.github.io/commit/d36baaf) como ejemplo de cómo se añadió una entrada anteriormente. Prueba localmente (abre index.html o corre Jekyll) antes de hacer push.

## Aplicar directo (Pablo lo aprobó el 2026-11-10)
Reorganizar la sección "Open Source Contributions" AGRUPANDO POR REPO (aprobado por Pablo), con las PRs mergeadas debajo de cada repo. Cada entrada lleva nombre, descripción corta, link y fecha. Mismo estilo terminal/interpretability del resto del sitio.

TODO 1. TransformerLens (TransformerLensOrg/TransformerLens), adaptadores de arquitectura TransformerBridge. Incluir #1478 Arcee squared-ReLU MLP (ArceeForCausalLM, ya en el sitio, mover bajo este grupo), #1483 RecurrentGemma (Griffin, ya en el sitio, mover bajo este grupo) y #1994 MiniCPM (MiniCPMForCausalLM, cierra #1992, NUEVA).

TODO 2. SAELens (decoderesearch/SAELens): #784 "fix: run the evals CLI on transformer-lens 4" (multiple_evals() usaba HookedTransformer, eliminado en transformer-lens 4.x). NUEVA.

## Quitar del sitio (orden explícita de Pablo, 2026-11-10)
TODO 3. Repo chemical-J-spaces: si aparece en "Repositorios" / "SELECTED WORK", eliminarlo. Está vacío (sin commits). No volver a incluirlo.

## No añadir todavía
TransformerLens #1998 (arreglo de un test float32): contribución menor. Pablo la dejó fuera; se guarda en state.json bajo "minor_contributions" para una posible métrica futura de "other minor contributions".
pyvene #242 (gradient checkpointing): abierta, sin mergear.
Forks (TransformerLens, pyvene, SAELens): no se listan.

## Al terminar
Actualiza `automation/state.json` marcando "applied" TransformerLens #1994 y SAELens #784.
