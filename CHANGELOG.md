# Changelog

## Unreleased

Fixes found after 1.0.0. The first public report, and the same kinds of mistake found elsewhere.

- **Every import saves its report as a file** (issues #2 and #3). `<name>_import_report.log` is
  written in the export folder, beside `<name>_export.json`, with the versions at the top and the
  error at the bottom when an import fails; a scene import writes `scene_import_report.log` in its
  folder. It is the file to attach to a bug report, and *Character > Import report* opens its
  folder.
- **A character on HS2's own skin shader imports textured.** Without Hanmen's Next-Gen shaders
  the body came in white and the face took the hair colour - the picture in issue #2. The body
  and face are now built from their own textures, plainly: without the skin's subsurface glow or
  the eyebrows yet. HS2's stock eyes get their eyeball texture but still have no iris.
- **The import report names every shader NS2BT has no recipe for yet**, with the materials on it,
  at the top of the report.
- **Hanmen's Eyes-for-V5 shaders are no longer built as the older Next-Gen eyes.** They were
  built with the Vanilla/Deepdive eye's formulas, which they do not share. Until they have their
  own recipe they are built plainly from their eyeball texture, without an iris, and the import
  report names them.
- **The report no longer says textures "overwrote each other"** when two materials share a name.
  The exporter keeps their files apart, and each material is built from its own - a decal layered
  over a garment of the same name now included.
- **A hair part made of two materials keeps both.** It was given its first material only, so the
  second piece drew with the first one's textures.
- **The import's closing message says when the viewport is in Solid view**, which shows flat
  colours and no textures.
- **Each character's materials are her own.** Editing inside a material group (Tab into "NS2BT
  Skin" and the rest) used to change every character in the file at once. Each character now gets
  her own copy of every group at import, so an edit changes only her. Characters imported before
  can be given theirs with *Make materials her own* on the deck's Attitude page. Props keep the
  shared groups.
- **Grass, bushes and other dense cut-out foliage no longer render black in Cycles.** A converted
  scene now allows 256 see-through bounces instead of Cycles' 8.
- **Mochie Standard's detail colour is read.** Maps that colour their grass or flowers through it
  (Photoshoot Room 3's lawn and blossom) were grey and white.
- **Sheer stockings on `Hanmen/Clothes True Transparent` are sheer.** They were built as a
  cut-out that kept every texel, so they rendered solid black.
- **Gloves and other clothing on `AIT/Clothes Alpha True BackCull` are built as cloth.** They were a
  flat placeholder, and are now see-through where the game's are.
- **Alloy's unlit shader is read.** A night-sky prop built on it was a black backdrop.
- **Bake to PBR.** On the deck's Attitude page, *Bake to PBR* turns a character's materials into
  plain PBR materials of her own: colour, roughness, normal, and metallic and alpha where she has
  them. The pictures are saved beside your file. Wetness and Blush keep working on the baked
  character. Eyes, tears and sheer garments stay live, since they change with the view. Her live
  materials are kept, and *Back to live materials* puts them back.
- **The Attitude page shows the two controls people use: Wetness and Blush** (Studio's Face
  flushing). Tears and Skin gloss moved to Developer mode; a saved file that uses them still works.
- **Eyes on characters from a parallel scene import read the scene's ambient light again.** Each
  appended character had brought its own copy of the ambient group, which the scene's light never
  reached.
- **A body without every face part now imports** (issue #1). Some body mods ship without the
  eyeshadow mesh, and the import stopped and rolled back. Missing parts are skipped now, and the
  import report names them.
- **Fitting a garment to a character imported with *Subdivision surface* no longer fails.**
- **Cloth on a subdivided body holds a hanging garment off the legs again.** It had silently
  stopped doing so, so skirts clung where they should hang.
- **A garment in an excluded collection** fails its own fit and says so, instead of stopping the
  import.
- **Enabling cloth survives a decal overlay with a damaged vertex.**
- **Clearing a physics bake made by an older version** no longer fails.
- **Batch and headless imports** no longer fail when nothing is selected.
- **Passes that put the active object back afterwards** no longer fail when it was deleted or
  hidden. These include the accessory bones, the eye split, the game export, and the Rigify bind,
  snap and unbind.
- The *Texture budget* and *Pack textures* options no longer print two warnings on every import.
- The *Strip imported clothing* report reads correctly.
- **The release is now checked by Blender's own extension validator.** The manifest's permissions
  line was shortened to Blender's limit.

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
