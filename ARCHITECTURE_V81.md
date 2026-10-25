# V81 Runtime Unification

## Goal
Remove the parallel constellation runtime Maps from the legacy viewer.

## Removed completely
- starPositionLists
- lineSegmentsByConstellation
- starMeshes
- lineMeshes
- constellationFirstStarPositions
- constellationLabelElements

## Single runtime structure
All constellation runtime/render state now lives under:

runtimeConstellationsV80[id]

Fields:
- starPositions
- segments
- center
- labelAnchor
- starMesh
- lineMesh
- artMesh
- labelElement

## Updated consumers
- selection visual state
- multi-constellation highlight
- sky-tap constellation candidate detection
- constellation labels
- constellation center
- line geometry refresh
- constellation artwork basis calculation

## Principle
Static source data and runtime objects are separated.
Runtime data is generated from canonical IDs and can be rebuilt.

## Still migration-era
- old retired info panel code still exists
- compatibility name normalization remains for legacy input data
- old precise artwork projection path still remains
- manga candidate list still remains

These are next-phase migration targets.
