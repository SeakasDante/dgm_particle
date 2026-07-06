# DGM Particle Creator

**DGM Particle Creator** is a desktop editor and 3D preview tool for GTA V particle effects (`.ypt` / `.ypt.xml`). Create, edit, and export custom particle FX for single-player modding, CodeWalker workflows, and **FiveM** servers — without hand-editing XML.

Developed by **Dogma Studio**.

---

## Support

Need help, found a bug, or want to share feedback?

**Join our Discord:** [https://discord.gg/8wGugUcz6n](https://discord.gg/8wGugUcz6n)

For license or purchase questions, use the Discord or your Tebex order email.

---

## Features

- **964+ indexed effects** from the vanilla `core.ypt.xml` library as starting points
- **3D real-time preview** with orbit camera, emit/target domains, attractors, and weapon-bone preview
- **Guided wizards** to create new effects and emitters step by step
- **Visual keyframe editor** — drag curve points, double-click to add, timeline recording
- **Emitter editor** — spawn rate, life, velocity, gravity, domains (box/sphere), and more
- **Texture dictionary** — browse, preview, and assign `.dds` textures to particles
- **Flipbook / atlas support** — animated sprite sheets with automatic GTA `UsageFlags`
- **Drawable (3D mesh) support** — import FBX/OBJ or use built-in primitives
- **Export `.ypt.xml`** — CodeWalker-compatible project files
- **Export binary `.ypt`** — ready for GTA V / OpenIV / CodeWalker
- **Export FiveM resource** — `fxmanifest.lua` + `stream/` folder in one click
- **Italian & English UI**

---

## Requirements

| Component | Notes |
|-----------|--------|
| **OS** | Windows 10/11 (64-bit) |
| **License** | Active Tebex license required for export (XML, YPT, FiveM) |
| **Textures** | `.dds` files in a texture folder (e.g. exported from CodeWalker) |
| **Binary export** | .NET 8 SDK (included in the portable build; needed only if building from source) |

Preview and editing work without a license. **Export is blocked until the license is activated.**

---

## Installation

1. Download the latest release from this repository (installer or portable `.exe`).
2. Run the installer, or extract/run the portable build.
3. On first launch, click **🔑 License** in the toolbar and enter your **Tebex Transaction ID** (`tbx-…`).
4. Set your **Texture folder** (toolbar → **Texture folder**) to a directory containing your `.dds` files.

The app checks for updates automatically on startup. You can also check manually from the **Save** tab.

---

## Quick start

### 1. Create or open a project

- **✨ Guided create** — step-by-step wizard for a new effect (fire, smoke, sparks, etc.)
- **New effect** — pick a template and name (this name is used in-game to spawn the effect)
- **Open XML** — load an existing `.ypt.xml` project

Effects marked with a green **★** border in the sidebar are **your custom effects** — only those are included when you export.

### 2. Edit in the viewport

- **Orbit:** hold mouse and drag
- **Move / Rotate / Scale domains:** use the viewport toolbar; click the blue emit sphere to scale particle size
- **Solo emitter:** preview only the selected emitter
- **Timeline:** scrub time, enable **● REC** to record keyframes as you tweak values

### 3. Assign textures

Open the **Texture** tab:

1. Click a texture in the list — it links to the current effect and appears in the 3D preview.
2. For animated flipbooks, set **Atlas columns × rows** (e.g. `4 × 4` for 16 frames).
3. Enable **GTA flipbook — auto UsageFlags**.
4. Choose animation mode: **Fire (fps)** or **Smoke (particle life)**.

### 4. Export

Open the **Save** tab and follow the numbered steps:

1. **Edit** your effect (Params, Keyframes, Texture tabs).
2. **Save `.ypt.xml`** — your editable project file.
3. **Choose texture folder** — must contain all `.dds` referenced by the project.
4. **Export `.ypt`** — binary file for GTA V / FiveM.
5. **Export FiveM resource** — full server-ready folder.

You can also use the toolbar shortcuts **Export XML** and **Export YPT** directly.

---

## Editor tabs

| Tab | Purpose |
|-----|---------|
| **Params** | Spawn count, life, emit domain, velocity, attractor — per emitter |
| **Timeline** | When each emitter starts/stops during the effect |
| **Behaviors** | Particle movement, colour, rotation, game flags |
| **Evolution** | Distance-based LOD variants |
| **Keyframes** | Time-based curves (size, colour, alpha, etc.) |
| **Texture** | Assign and configure `.dds` / flipbook atlases |
| **Drawable** | 3D mesh particles (optional) |
| **Save** | Export XML, YPT, FiveM resource, updates, flipbook audit |

Use **◎ viewport** on collapsed sections in the Params tab to focus the 3D gizmo on that domain.

---

## Flipbook animations (animated textures)

GTA V animates flipbook textures using **clip regions** from the vanilla `ptxclipregions.dat`. The game only applies these regions when the texture **name matches a vanilla entry** with the same atlas grid.

**DGM Particle Creator handles this automatically on export:**

- Your custom flipbook `.dds` content is kept as-is.
- The texture is **renamed to a compatible vanilla name** (e.g. `ptfx_muzzle_core_rgb` for a 4×4 grid) in both the `.ypt` and the copied `.dds` filename.
- No custom `.dat` file is needed — FiveM ignores custom clip-region files for non-vanilla names.

Before exporting, run **Flipbook debug** in the Save tab to verify `UsageFlags`, `AnimateTexture`, frame range, and the chosen vanilla rename.

**Tip:** If you use several flipbooks with the **same grid size** in one export, each gets a different vanilla name. If you run out of available names for that grid, merge atlases or split into separate resources.

---

## FiveM export

**Export FiveM resource** creates a folder like this:

```
my_resource/
├── fxmanifest.lua
├── README.txt
└── stream/
    ├── my_resource.ypt
    └── *.dds
```

**To use on your server:**

1. Copy the folder into your server's `resources/` directory.
2. Add to `server.cfg`: `ensure my_resource`
3. Spawn the effect in-game using your custom effect name (e.g. with `START_PARTICLE_FX_NON_LOOPED_AT_COORD` or your framework's particle API).

The generated `fxmanifest.lua` and `README.txt` list any flipbook texture renames applied during export.

**Important:** Make sure the **Texture folder** is set and contains all required `.dds` files before exporting. Missing textures will block the FiveM export.

---

## CodeWalker live preview

1. Open CodeWalker → **Menu → YPT Live Bridge**.
2. In DGM Particle Creator, open the **Save** tab and enable **Send changes to CodeWalker in real time**.
3. Edits are pushed to CodeWalker automatically for in-engine preview.

---

## License activation

1. Click **🔑 License** in the toolbar.
2. Enter your **Tebex Transaction ID** from your purchase confirmation email (`tbx-…`).
3. Click **Activate**.

Export features require an active license. The status bar shows remaining days when activated.

---

## Troubleshooting

| Issue | What to check |
|-------|----------------|
| Textures not visible in preview | Set **Texture folder** and ensure `.dds` filenames match the XML |
| Export blocked | Activate your license (**🔑 License**) |
| YPT export fails | Texture folder must contain all referenced `.dds` files |
| FiveM flipbook not animating | Run **Flipbook debug**; confirm atlas grid matches frame count; re-export so vanilla rename is applied |
| Effect not spawning in FiveM | Verify `ensure` in `server.cfg` and use the exact custom effect name from the sidebar |
| Wrong flipbook frames in-game | Grid cols×rows must match your atlas; check the rename mapping in the export message |

If you are still stuck, ask on **[Discord](https://discord.gg/8wGugUcz6n)** with your effect name, atlas grid, and export log message.

---

## Language

**⚙ Settings** → switch between **Italian** and **English**. The choice is saved automatically.


---

## Links

- **Support & community:** [Discord — Dogma Studio](https://discord.gg/8wGugUcz6n)
