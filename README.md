# TouchGrass modular

Refactor de interfaz de TouchGrass V11.5. La lógica de simulación, `GameState`, `SAVE_KEY`, migraciones, IndexedDB, `SaveManager` y `SimulationEngine` se conservan dentro de `src/legacy/touchgrass-engine.js`.

## Ejecutar

Sirve esta carpeta con un servidor HTTP:

```bash
python -m http.server 8000
```

Abre `http://localhost:8000/`. No abras `index.html` con `file://`, porque las vistas usan módulos ES y carga dinámica.

## GitHub Pages

Publica el contenido de esta carpeta en el repositorio `touchgrass`. `404.html` y los pequeños índices de ruta restauran enlaces directos como `/touchgrass/vida` o `/touchgrass/educacion`.

## Arquitectura

- `src/legacy/touchgrass-engine.js`: motor y compatibilidad histórica sin reescritura.
- `src/app/Router.js`: History API, atrás/adelante, enlaces directos y restauración.
- `src/app/UIRuntime.js`: adaptador de render; actualiza la cabecera y solo la vista activa.
- `src/app/domPatch.js`: parcheo incremental de nodos; evita reemplazar contenedores completos y conserva nodos/listeners cuando su estructura no cambia.
- `src/ui/views/`: módulos con `render()`, `update()` y `destroy()` heredados de `ViewBase`.
- `src/app/ThemeManager.js`: preferencias visuales separadas de `GameState`.
- `src/styles/themes.css`: diez temas completos.
- `COMPATIBILITY.md`: invariantes de estado, guardado y migraciones.
- `tests/invariants.mjs`: comprobación estática reproducible (`node tests/invariants.mjs`).

## Compatibilidad

Clave de guardado original: `vida_rng_save_v3`. Base IndexedDB original: `vida_rng_v117_saves`. Las preferencias de apariencia usan otra clave (`touchgrass_ui_preferences_v1`) para no modificar el estado de la partida.

Fuente original SHA-256: `1a81aca252555f604694c024d2c2f45f46afccc68e6197e7387eedde11815b23`
