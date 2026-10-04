# NS2BT - Neo Studio 2 Blender Toolkit

Take a Honey Select 2 **StudioNEO V2** scene into **Blender 5.2**: characters posed where Studio
had them and rigged with Rigify, their materials rebuilt from what Studio exported, hair and body
physics running on the game's own numbers, and the props, cameras, lights and map around them.

**Version 1.0.0 · Windows 64-bit · Blender 5.2 or later**

**[Download the latest release](https://github.com/MrOvis3000/NS2BT-Neo-Studio-Blender-Toolkit/releases/latest)**
(`NS2BT-1.0.0.zip`, both halves in one zip)

---

## What it does

NS2BT has two halves. A **Studio plugin** exports from the running Studio (press **F10**), and a
**Blender extension** imports what it exported. They share nothing but the export folders.

- **Characters** arrive at their real height, posed as in Studio and bound to a Rigify control rig
  (FK and IK). Their materials are rebuilt from the values Studio's shaders actually used, with
  Hanmen's Next-Gen shaders understood in detail. Face expressions, gaze and the game's Attitude
  sliders come across as controls.
- **Physics** is the game's own. Every dynamic-bone chain (hair, breasts, skirts, tails, ears) is
  re-simulated in Blender from the numbers the character had in Studio. On top of that:
  - body types: Average, Muscular, Soft, or the game's own;
  - an optional soft body for thighs, hips and arms;
  - Blender cloth for any garment.
- **Scenes** bring every character, prop, camera and light, the map, and the Studio look (bloom and
  exposure as one compositor node you can tune or delete). Importing the same scene again updates
  it in place and keeps your own edits.
- **Live with Studio:**
  - *Watch for Studio exports* imports whatever Studio exports as it lands.
  - The Prop and Pose Browsers put Studio's items and poses in Blender's Asset Browser.
  - The Wardrobe changes a character's clothes through the running Studio without re-exporting her.
  - Studio's animations are recorded and baked onto the rig.
- **The deck** is a control panel inside the viewport for the selected character. Its pages cover
  face, presets, pose, animations, physics, attitude and clothes, each with hover help.

## What you need

| | |
| --- | --- |
| Honey Select 2 with **BepInEx 5.4**, **IllusionModdingAPI** and **Sideloader** | A BetterRepack install has all three |
| **Grey's HS2 MeshExporter** (`BepInEx\plugins\HS2MeshExporter\`) | Required: NS2BT drives it to write the FBX. An optional part of BetterRepack |
| **Blender 5.2** or later, Windows 64-bit | It will not install on 4.x |
| XUnity AutoTranslator, AdvancedItemSearch | Optional: English item names and pictures in the Prop Browser |

## Install

1. **Studio plugin.** Close Studio. Copy the zip's `Studio\BepInEx` folder into your HS2 folder
   (the one that holds `abdata`), merging folders. Start Studio and check
   `BepInEx\LogOutput.log` for *"NS2BT HS2 Exporter 0.1.0 ... ready. Press F10 ..."*.
2. **Blender extension.** In Blender: *Edit > Preferences > Get Extensions*, the arrow at the top
   right, **Install from Disk**, and pick `Blender\ns2bt-0.1.0.zip` from the zip.
3. **Two settings.** In *Edit > Preferences > Add-ons > NS2BT*:
   - set **HS2 install** to your HS2 folder;
   - press **Set up**, which switches on Rigify (it ships with Blender).

## First use

1. **In Studio**, press **F10**:
   - **Export Scene** exports the whole shot: characters, props, map, cameras and lights.
   - **Export Characters** exports every character, one folder each.

   Exports land in `<HS2>\Export\`.
2. **In Blender**, press `N` in the 3D viewport and open the **NS2BT** tab. Use **Import Scene**
   and pick the `<time>_scene_<name>` folder, or **Import Character** and pick a character's
   folder.
3. **Deck > Open Deck** puts the character controls in the viewport.
4. Every import writes a report: *Character > Import report*, and the same as a file,
   `<name>_import_report.log`, in the export folder beside `<name>_export.json` (a scene import:
   `scene_import_report.log` in the scene's folder, and the *NS2BT Scene Report* text block).
   Anything it could not do is named there, most important first.
5. Materials show in **Material Preview** (`Z`) or a render; Solid view draws flat colours.

The full manual is inside Blender: **NS2BT tab > Help > Open the manual**.

## Updating

Close Studio and replace the DLL. In Blender, install the new zip over the old one, then
**restart Blender**: a running Blender keeps the code it loaded.

## Known limits

- Built and tested against Hanmen's Next-Gen shaders and the mods of one HS2 install. A material
  on a shader NS2BT has never seen comes in plain, and the import report names the shader.
- Big scenes are texture-heavy. If a render crashes Blender, set a **Texture budget** of 4096 on
  the import dialog.
- These have had the least testing, so reports on them are especially welcome:
  - the Wardrobe;
  - prop physics;
  - *Record All Animations*;
  - the glTF game export;
  - *Watch for Studio exports*;
  - linking one character into several scenes;
  - garments on cloth.

## Reporting a problem

Open an issue on GitHub (*Issues > New issue > Bug report*) and **attach the import report**.
Without it, most problems cannot be traced.

1. **Find the export folder:** `<HS2>\Export\<timestamp>_<name>\`. In Blender,
   *Character > Import report > Open its folder* opens it.
2. **Attach the import report:** `<name>_import_report.log` in that folder. Every import writes it,
   a failed one too; a scene import writes `scene_import_report.log` in the scene's folder. Drag
   the file into the issue.
3. **Attach the export's JSON from the same folder:** `<name>_export.json` (what the exporter
   worked around), and for a material or texture problem `<name>_materials.json`.
4. **For an export problem,** attach `<HS2>\BepInEx\LogOutput.log` too.
5. **Say what you did, and your Blender version.** A screenshot helps. Missing textures? Check
   that the viewport is in Material Preview (press `Z`): Solid view shows flat colours.

NS2BT 1.0.0 does not write the report file yet: copy *Character > Import report > Whole report in
the Text Editor* into the issue instead, or for a failed import the system console (*Window >
Toggle System Console*).

The report and the JSON are enough in most cases. Please don't send characters or textures you
don't have the rights to share.

## Credits

- **Grey**, whose HS2 MeshExporter writes the FBX NS2BT builds on.
- **Hanmen**, whose Next-Gen shaders NS2BT reads the parameters of.
- **BepInEx**, **IllusionModdingAPI** and **Sideloader**.
- **UnityPy** and the other bundled Python packages; each one's licence is in the extension.
- Blender's **Rigify**.

NS2BT is free to use. Please link to this page rather than re-uploading the zip, so everyone gets
the fixes.
