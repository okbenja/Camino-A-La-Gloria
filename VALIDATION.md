# Validación realizada

## Resultado

- Sintaxis válida en todos los archivos JavaScript de `src/`.
- 15 rutas con vistas cargadas mediante `import()` y clases válidas.
- 14 módulos físicos de vista; `SettingsView` sirve `/configuracion` y `/configuracion/apariencia`.
- Una sola `.route-panel` montada durante los cambios de ruta probados.
- Creación de partida V11.5 correcta en una VM aislada.
- Estado validado por `validateStateV11`: sin errores, sin referencias inválidas.
- 64 claves de estado tras crear la partida, sin cambios al aplicar preferencias visuales.
- Prueba interna `TouchGrass.runV115Tests()`: 10/10 comprobaciones aprobadas.
- Parcheo incremental comprobado: un nodo no modificado conserva su identidad tras `update()`.
- Diez temas y sus preferencias persistentes comprobados.
- Comparación contra el script original: cinco bloques distintos, correspondientes únicamente a cuatro montajes eager desactivados y al inicializador sustituido por el puente modular.

## Persistencia comprobada

- `SAVE_KEY`: `vida_rng_save_v3`.
- IndexedDB: `vida_rng_v117_saves`.
- Store: `states`.
- Registro: `main`.
- Marcador: `V117_INDEXED_DB`.

## Pruebas reproducibles

```bash
node tests/invariants.mjs
```

El entorno de validación bloqueó por política administrativa la navegación HTTP real hacia dominios de prueba. Por eso el montaje de vistas se probó en Chromium con el documento y los módulos inyectados, mientras que History API, `popstate`, `pushState`, `replaceState`, normalización de rutas y fallbacks de GitHub Pages se verificaron por código y pruebas estáticas.
