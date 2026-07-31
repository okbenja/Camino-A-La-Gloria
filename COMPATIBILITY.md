# Compatibilidad y límites de la refactorización

## Invariantes preservados

- `GameState`: se conserva la función `baseState()` y su forma original. Las preferencias visuales no se agregan al estado.
- `SAVE_KEY`: `vida_rng_save_v3`.
- IndexedDB: base `vida_rng_v117_saves`, store `states`, registro `main` y marcador `V117_INDEXED_DB`.
- Se mantienen las clases y cadenas de envoltura existentes de `SaveManager`, `MigrationManager` y `SimulationEngine`.
- Se mantienen las validaciones, compresión, respaldos, importación/exportación y migraciones V10/V11/V11.5–V11.9 incluidas en el archivo original.

## Cambio controlado

El script original fue trasladado a `src/legacy/touchgrass-engine.js`. La comparación con el HTML fuente arrojó solamente cinco bloques diferentes:

1. Se desactivaron cuatro llamadas de montaje eager de la interfaz (`installV10UI`, `installV11UI`, `installV119UI`, `installTouchGrassUI`). Sus funciones siguen presentes.
2. El inicializador final fue reemplazado por un puente de UI y por `src/app/bootstrap.js`.

La lógica de juego anterior a ese punto permanece en el mismo orden. El puente redirige `render`, `renderEvent`, `switchPanel` y `openSettings` hacia la vista activa sin recrear el mundo ni volver a cargar el guardado.

## Preferencias visuales

Se almacenan en `touchgrass_ui_preferences_v1`, separadas de la partida. Así se evita modificar las claves del estado o exigir una nueva migración.

## Comprobaciones incluidas

Ejecutar desde la raíz:

```bash
node tests/invariants.mjs
```

El test verifica claves de persistencia, presencia de motor y gestores, carga dinámica de rutas, ciclo de vida de vistas, temas, fallback de GitHub Pages y la instalación del parcheo DOM incremental.
