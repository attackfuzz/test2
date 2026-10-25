# V80 Core Architecture — Phase 1/2

## Canonical source
- `CONSTELLATIONS_V2`: 88 constellation master
- object key = only internal ID (`uma`, `cma`, `cvn`, ...)
- canonical fields: `iau`, `en`, `ja`, `aliases`, `groups`

## Runtime model
- `runtimeConstellationsV80[id]`
  - `starPositions`
  - `segments`
  - `center`
  - `labelAnchor`
  - `starMesh`
  - `lineMesh`
  - `artMesh`
  - `labelElement`

## State
- `ViewerStateV80.selectedConstellationId` is the source of truth for current constellation selection.

## Selection
- `selectConstellationV80(id, options)` is the canonical constellation selection entry point.
- Search and sky-tap selection now use this entry point.
- The old `<select>` is presentation/compatibility UI, not the source of truth.

## Renderer keys
- Star meshes, line meshes, line segments, star position lists, labels are now keyed by lowercase internal ID.
- Legacy display strings such as `Ursa Major (おおぐま座)` are no longer renderer keys.

## Migration bridge
The following legacy names are temporarily accepted only as input aliases:
- old IAU IDs
- English names
- old Japanese names from `stars.js`
- old combined renderer labels

They are normalized once by `ConstellationRegistryV80`.
New core code does not create new legacy keys.

## Next phase
- remove remaining legacy selection/info code
- consolidate old parallel Maps into `runtimeConstellationsV80`
- migrate artwork basis to V80 runtime
- replace manga candidate list with `<id>_manga.png`
- remove legacy filename probing
