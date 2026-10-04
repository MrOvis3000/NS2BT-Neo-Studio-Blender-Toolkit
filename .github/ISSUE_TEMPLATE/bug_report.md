---
name: Bug report
about: Something went wrong exporting from Studio or importing into Blender
title: ""
labels: bug
---

**What happened**
<!-- What you did, and what went wrong. A screenshot helps. Missing textures? Check the viewport
is in Material Preview (press Z) - Solid view shows flat colours and no textures. -->

**What you expected**

**Versions**
- NS2BT (Blender: *Edit > Preferences > Add-ons > NS2BT*, or `LogOutput.log`'s "NS2BT HS2 Exporter" line):
- Blender:
- HS2 setup (BetterRepack? which shader packs?):

**Please attach** (from the export folder, the `<timestamp>_<name>` folder in `<HS2>\Export\`,
unless said otherwise)
- The **import report**: **`<name>_import_report.log`**, which every import writes there, a failed
  one too (a scene import: `scene_import_report.log` in the scene's folder). NS2BT 1.0.0 does not
  write the file: use *Character > Import report > Whole report in the Text Editor* and paste the
  text block *NS2BT import report - <name>*, or for a failed import the system console
  (*Window > Toggle System Console*).
- **`<name>_export.json`** (it lists what the exporter worked around).
- For a material or texture problem: **`<name>_materials.json`** (each material's shader and
  texture files - no pictures).
- For an export problem: **`LogOutput.log`**, in the HS2 folder itself: `<HS2>\BepInEx\LogOutput.log`.

These files are enough in most cases. Please don't attach characters or textures you don't have
the rights to share.
