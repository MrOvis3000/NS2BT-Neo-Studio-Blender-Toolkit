# Changelog

## 1.0.0 - 2026-09-30

Out of beta. Everything the beta shipped, plus what the first day of use turned up.

- **Maps that Unity static-batched now arrive.** Their geometry lives only on the GPU, so the
  exporter cannot read it and says so; the same mesh is read back from the map's own `.zipmod`
  instead. A set that imported as bare empties, floor included, now imports whole.
- **Chain colliders land where they can be seen.** *Add collider* placed the empty at the 3D
  cursor, which for a character standing where Studio put her is usually far off screen; it now
  goes to the character when the cursor has not been moved, and is selected so *Frame Selected*
  reaches it.
- The scene report no longer swallows the exporter's `unreadable_mesh` warning.

## 0.1.0 beta - 2026-09-29

The first public beta.

- **Studio plugin** (F10 in StudioNEO V2): export the whole scene, every character on its own,
  or the selected props; save the current poses; write Studio's item catalogue.
- **Blender extension** (Blender 5.2): import a scene, a character or a prop.
  - Characters are posed, at their real height, on a Rigify control rig.
  - Materials are rebuilt from the values Studio's shaders used, with Hanmen's Next-Gen shaders
    in detail.
  - The game's dynamic bones are re-simulated, with body types, soft body and cloth on top.
  - Props, cameras, lights, the map and the Studio look come with the scene.
  - Live links to Studio: auto-import, the Prop and Pose Browsers, the Wardrobe, and recorded
    animations.
  - The deck: the character's controls in the viewport.

See the README's *Known limits* for what has had the least testing.
