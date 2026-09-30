# Installing NS2BT

> This is the manual that ships inside the extension (*NS2BT tab > Help > Open the manual*).
> Download the release zip from the [releases page](https://github.com/MrOvis3000/NS2BT-Neo-Studio-Blender-Toolkit/releases/latest).

This page is for a developer setting NS2BT up on their own machine: a Honey Select 2 install with
StudioNEO V2, and Blender 5.2. NS2BT has two halves. The **Studio plugin** exports a scene, a
character or a prop out of the running Studio. The **Blender extension** imports it. They are
installed separately and talk only through the export folders (and, for the Prop Browser, through
the files in `<HS2>/NS2BT_Library/`).

## What you need

| Component | Required | Notes |
| --- | --- | --- |
| Honey Select 2 with **BepInEx 5.4** | yes | A BetterRepack install has everything in this column |
| **IllusionModdingAPI** (`HS2API.dll`) | yes | Names, mod lookups |
| **Sideloader** (`HS2_BepisPlugins`) | yes | Mod items and their GUIDs |
| **Grey's HS2 MeshExporter** (`BepInEx/plugins/HS2MeshExporter/`) | yes | NS2BT drives it to write the FBX; without it no export works |
| XUnity AutoTranslator | no | English names for Studio's Japanese ones (Prop Browser) |
| AdvancedItemSearch, `[STN] StudioThumb.zipmod` | no | The item pictures the Prop Browser shows |
| **Blender 5.2** (Windows x64) | yes | 5.2.0 or later; NS2BT is pinned to the 5.2 LTS |
| **Rigify** (ships with Blender) | yes | Off until enabled; every import binds the character to it. *Set up* enables it |
| Retarget (extensions.blender.org) | no | The step past NS2BT's own Mixamo retarget. *Set up* installs it |

## 1. The Studio plugin

Copy **`HS2Exporter.dll`** to

```text
<HS2>\BepInEx\plugins\NS2BT\HS2Exporter\HS2Exporter.dll
```

Close Studio first: Windows locks a loaded DLL, and a copy over it fails. To check that the
plugin is the one you copied, start Studio and look in `<HS2>\BepInEx\LogOutput.log` for:

```text
NS2BT HS2 Exporter 1.0.0 (build 2026-09-28 09:00:00) ready. Press F10 for the NS2BT export menu.
```

The build stamp is when the DLL was compiled. It is how you tell an old copy from a new one.

## 2. The Blender extension

In Blender: **Edit > Preferences > Get Extensions > (the arrow, top right) > Install from Disk**,
and pick **`ns2bt-1.0.0.zip`** (the version in the name changes with each release). An **NS2BT**
tab appears in the 3D viewport's sidebar (`N`). This manual is inside it too: **Help > Open the
manual**.

Then set **one preference**: *Edit > Preferences > Add-ons > NS2BT > **HS2 install***, the game
folder (the one that holds `abdata/`, `mods/`, `UserData/`). Everything else is found from it:
the export folders, the pose library, the saved poses, the item catalogue. If you skip it, NS2BT
finds the install from the first character you import, but the Prop and Pose Browsers need it
before that.

**Then press *Set up***, at the top of the same preferences page. It lists what NS2BT uses and
does not ship - Rigify and Retarget - with each one's state; one press enables what
is installed and installs what is missing. Installing comes from extensions.blender.org and needs
Blender's *Allow Online Access* (Preferences > System > Network), which *Set up* never switches
on for you: the page shows Blender's own button for it when it is off. Offline, Rigify - the one
an import needs - is enabled anyway, since it ships with Blender. If you import before pressing
*Set up*, the import switches Rigify on by itself and says so in the first line of its report.

**After updating the extension, restart Blender.** A running Blender keeps the modules it loaded
at startup, so the old code keeps running until it restarts. Reload Scripts is not enough for
everything.

## 3. The buttons

In **Studio**, press **F10** for the NS2BT menu (F1 > Plugin Settings to rebind it):

- **Export Scene** - the whole scene: every character, prop, camera, light and the map. This is
  the one to use.
- **Export Characters** / **Export Selected Props** - every character in the scene, each in a
  folder of its own, or the props selected in the workspace tree, on their own.
- **Save Current Poses** - each character's current pose, for the Pose Browser.
- **Write Item Catalogue** - Studio's item list, for the Prop Browser. It also writes itself a few
  seconds after Studio loads.

Exports land in `<HS2>\Export\<timestamp>_<name>\`.

In **Blender**, the **NS2BT** tab of the sidebar (`N`) holds six panels, most-used first:
**Studio** (the imports and the watch switch), **Deck**, **Character** (what acts on the
selected character, in sub-panels), **Physics**, **Libraries** and **Help**. Under **Studio**:

- **Import Scene** - pick the scene's export folder (`<timestamp>_scene_<name>`). Characters
  come in posed where Studio had them, Rigify-rigged, with the props, cameras, lights, the map
  and the Studio look (bloom and exposure as one compositor node, *NS2BT Look*, to dial or
  delete). Importing the same folder again updates the scene in place: nothing is
  duplicated, and your own edits and added lights are kept.
- **Import Character** / **Import Prop** - one export folder, the one that directly holds
  the `.fbx`. A character and a prop use different buttons on purpose. Pointed at the other's
  folder, each one fails.
- **Watch for Studio exports** - with it on, everything Studio exports comes into the current
  scene by itself: a scene this file already holds is updated in place, and any other scene, a
  character (*Export Characters*) or a prop (*Export Selected Props*) is imported. Nothing asks
  first. Off at every start of Blender; it needs the HS2 install set in the preferences. Only
  while Studio is open, and only an export from the last ten minutes: an older one is left for
  the Import buttons, and the panel says *Studio is closed* while nothing can be taken.
- **Wardrobe** - change a character's clothes, hair and accessories, or load an outfit card,
  without exporting her again. Open it once from **Libraries** (it builds itself), then
  double-click an item in the Asset Browser's **NS2BT Wardrobe** library, or use the
  **Wardrobe** section of the deck's **Clothes** page (*Change*, *Remove*, *Add accessory*,
  *Original outfit*). Studio must be open with the plugin. Studio dresses her - in the item's own
  colours - and sends only what changed; her pose and everything else stay as they are. If she is
  not in the open scene, Studio adds her from the card saved with her export (exports from before
  the wardrobe have none: export her once more). A character linked from a library file changes
  in that file.
- **Export for Game (glTF)** - in the character's *Reuse this character* panel and under
  *File > Export*: every material baked to base colour, normal and roughness pictures, and the
  character written as one `.glb` (skin, deform bones, shape keys) for a game engine. Minutes,
  since every material is baked; her materials in Blender are left as they are.
- **A character in more than one scene** - save her `.blend` once she is set up, and bring her
  into any scene with Blender's own *File > Link* or *Append* (or mark her as an asset: *Reuse
  this character* > *Mark as Asset*). NS2BT does not manage this for you (D247).
- **Prop Browser** / **Pose Browser** / **Expressions** - every Studio item, pose and HS2PE
  expression in Blender's Asset Browser (`docs/prop_library.md`, `docs/pose_library.md`). Each
  builds itself the first time it is opened from **Libraries**, and again when Studio's list
  has changed since; *Rebuild* is in the add-on's preferences. The expressions are filed
  by head variant with the lip-sync set apart; their names come from a file NS2BT writes the
  first time (`<Blender user data>/ns2bt/face_names.json`) which you can edit; *Save this face*
  on the deck's Presets page keeps a face of your own under *Mine*, and *Render pictures* gives
  them the character's face as pictures.
- **Anims** - every animation in Studio's Anim menu, by Studio's own group and category. It
  needs Studio to have been opened once with the plugin (it writes the list). Double-click
  one with a character selected to bake it onto her from the current frame, on her Rigify
  controls; one not recorded yet is recorded through the running Studio first. To have them all
  without Studio, press F10 → *Record All Animations* in Studio once (it can be stopped and picks
  up where it stopped).

**The import dialog** opens with the options most imports want already set. **Skin detail** is
how strongly pores and skin relief show (0 smooth, 1 the game's); the deck changes it later. Face
morphs, the Rigify switch, triangles to quads, the eye parts and **Character units** are under the
closed *Advanced* section; each is right for nearly every import. Character units (on) brings her
in at her real height, 1 Blender unit = 1 metre, and the report gives her height in cm; off keeps
Studio's own scale, about ten times life size, and is only for matching coordinates read out of
Studio - the materials' light scattering, the gaze targets, Mixamo retargeting and Rigify's root
widget assume metres. The defaults for both are in NS2BT's preferences.

## 4. Working on a character: the deck

**Deck > Open Deck** (sidebar) puts NS2BT's control surface in the viewport: drag it by its title,
resize it from the bottom-right corner, hover a control for what it does. **Open Control Window**
gives it a window of its own for a second monitor. It acts on the selected character. The pages:

- **Face**, **Presets**, **Pose** - her face's dials, expressions and saved faces, and posing
  (FK / IK on the Rigify rig).
- **Anim** - *Her animations* lists every animation made for her; click one to put it on, and
  **Take off** stops her (the animation stays in the file). A new animation **loops** by default
  (*Loop On / Off*), and the timeline grows to hold it, never shrinks. Putting another animation
  on clears a physics bake, which only fits the animation it was baked on.
- **Physics** - **Live** runs the simulation as the timeline plays; **Bake…** keys it over the
  frames you choose. **Body** sets what her whole body is made of: **Average** (the default, a
  little livelier than the game's own breasts), **Muscular** (less motion), **Soft** (more) or
  **Game** (the export's own numbers). *Made of* on each section and chain overrides it there.
  The materials' numbers are in *Preferences > NS2BT > Physics materials*, with a button to put
  the researched values back; a character already made of a body keeps its numbers until a body
  is picked again. A body mod's belly chain is left to the animation.
- **Attitude** - where her eyes look (**Gaze**), the game's Attitude sliders, and **Skin detail**.
- **Clothes** - **On / Half / Off** for each slot; **Show all** puts every slot in its full state,
  **Hide all** hides everything. **Garment…** and **Fit selected** add a garment from outside HS2
  and fit it to her. Under **Slots**, **Cloth** puts a garment on Blender's cloth: its fabric,
  tightness, bands, elasticity and skin gap are dials there, **Warm-up** lets it settle before the
  shot, and **Bake** asks which frames to simulate and keeps the result (**Free bake** lets go of
  it, to change the dials). **Select cage** shows and selects the mesh the cloth runs on, for
  Blender's own Cloth panel; it hides again when you select anything else.

## 5. The import report

Every import writes what it did into **Character > Import report** (and the system
console). The lines that mean something is wrong are at the top:

- *"... is not exported"*, *"has no export folder"* - Studio could not export that subject. It is
  named, not silently dropped. Export it again, or check the Studio log.
- *"composed in Studio's map ..."*, then *"the map's geometry is not exported yet"* - the scene
  was built on a map this export does not carry. The characters, props, cameras and the map's own
  lights are all there. *"no Studio map"* means the scene was built on the empty set.
- *"hung off ... which is not in this import"* - a parented item whose parent did not come
  across. It stays where Studio had it.
- *"in its Studio pose (N bones, worst X mm off)"* - how close the pose landed. Under a millimetre
  is normal.
- *"export: ..."* lines are the exporter's own notes (a particle system, a playing animation):
  things a Blender file cannot hold, said once.

## When something is off

- **The fix you just installed does not show.** Restart Blender (for the extension), or check the
  build stamp in `LogOutput.log` (for the plugin).
- **An export fails at once.** Grey's MeshExporter is missing or failed to load. Check
  `LogOutput.log` for `HS2MeshExporter`.
- **Blender crashes during a render.** Check the Windows event log for a GPU driver reset before
  suspecting NS2BT. A scene with seven characters is texture-heavy for EEVEE: the scene import's
  *Texture budget* at 4096 px took one from 10.5 GB of textures to 6.3 GB, a change no one can see
  (the import dialog, or the add-on preferences for every import).
