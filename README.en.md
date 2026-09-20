# Young Handsome Desktop Pet 🏀

**Meet Young Handsome, your basketball companion while you code.**

[简体中文](README.md) | **English**

![Codex Pet](https://img.shields.io/badge/Codex-Pet-222222) ![Sprite Format v2](https://img.shields.io/badge/Sprite_Format-v2-blue) ![WebP](https://img.shields.io/badge/Atlas-WebP-green)

Young Handsome is a basketball-themed pet character pack for the **Codex desktop app**, containing a character manifest and a sprite atlas. Install it in your local pets directory, then select it in a desktop client that supports custom pets.

[Preview](#preview) · [Quick Start](#quick-start) · [Customization](#customization) · [FAQ](#faq) · [Contributing](#contributing)

<a id="preview"></a>

## Preview

![Young Handsome displayed on the desktop](screenshots/demo.png)

A chibi character in a basketball jersey brings a sporting companion to your desktop.

[View the character reference image](assets/YoungHandsome.jpg)

## Character Features

- **Basketball-inspired design**: a chibi character based on the Young Handsome reference image.
- **Transparent sprite atlas**: a WebP asset measuring `1536 × 2288` pixels.
- **v2 pet format**: the manifest uses `spriteVersionNumber: 2`, with an 8-column × 11-row atlas and `192 × 208` cells.
- **Local installation**: the pack consists of one JSON manifest and one WebP atlas. No Node.js, Python, or build dependencies are required for this repository.

This repository provides the character artwork and animation assets. The host app provides the floating window, dragging, show/hide controls, task status, and other interactions. Behavior depends on your client version and settings.

<a id="quick-start"></a>

## Quick Start

### 1. Prepare the Desktop App and Download the Pack

Install a Codex desktop client that supports custom pets and v2 sprite atlases. The instructions below use Windows. See the [official OpenAI pets documentation](https://learn.chatgpt.com/docs/pets) for pet settings and display controls. The desktop product name and menu wording in the official documentation may differ from your installed version.

On this repository's page, select **Code → Download ZIP** and extract the archive, or use Git:

```powershell
git clone https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet.git
cd YoungHandsome-Desktop-Pet
```

### 2. Install the Character Pack

**Copy the files manually**

1. Enter `%USERPROFILE%\.codex` in the File Explorer address bar. If you have set `CODEX_HOME`, open the directory specified by that environment variable instead.
2. Create a `pets\young-handsome` folder inside it, creating any missing parent directories as needed.
3. Copy **both `pet.json` and `spritesheet.webp`** from the downloaded repository's `character` folder into `young-handsome`.

The default installation should look like this:

```text
%USERPROFILE%\.codex\pets\young-handsome\
├── pet.json
└── spritesheet.webp
```

Both files must be in the same directory. Do not add another `character` folder inside `young-handsome`. If `CODEX_HOME` is set, the destination is `<CODEX_HOME>\pets\young-handsome\`.

**Or use PowerShell**

Open PowerShell in the **root of the downloaded or cloned repository** and run the following commands. They use `CODEX_HOME` when set, falling back to `.codex` in your user directory. Running them again updates these two files in the existing character pack.

```powershell
$petHome = if ([string]::IsNullOrWhiteSpace($env:CODEX_HOME)) {
    Join-Path $env:USERPROFILE '.codex'
} else {
    $env:CODEX_HOME
}
$petDirectory = Join-Path $petHome 'pets\young-handsome'
New-Item -ItemType Directory -Path $petDirectory -Force | Out-Null
Copy-Item -LiteralPath '.\character\pet.json', '.\character\spritesheet.webp' -Destination $petDirectory -Force
```

### 3. Select and Show Your Pet

1. Open **Settings → Pets** in the desktop app.
2. Select **Refresh**, then choose **Young Handsome**.
3. Enter `/pet` in the chat input, or select **Show pet** from the command menu.

If the list has not updated, restart the desktop app and check again. Young Handsome is now ready to join you on your desktop.

## Repository Structure

```text
YoungHandsome-Desktop-Pet/
├── assets/
│   └── YoungHandsome.jpg    # Character reference image
├── character/
│   ├── pet.json             # Character manifest
│   └── spritesheet.webp     # v2 sprite atlas
├── screenshots/
│   └── demo.png             # Desktop preview
├── .gitignore
├── LICENSE
├── README.md                # Chinese guide (default)
└── README.en.md             # English guide
```

Only the two files in `character` are needed for installation. The reference image and screenshot are included for presentation.

<a id="customization"></a>

## Customization

The character manifest is [`character/pet.json`](character/pet.json):

| Field | Current value | Purpose |
| --- | --- | --- |
| `id` | `young-handsome` | Character identifier; use a new identifier and a matching installation folder for a separate variant |
| `displayName` | `Young Handsome` | Name shown in the pet picker |
| `description` | English character summary | Describes the character's theme and appearance |
| `spriteVersionNumber` | `2` | Sprite format version; must match the atlas layout |
| `spritesheetPath` | `spritesheet.webp` | Atlas path relative to `pet.json` |

Keep the JSON valid when editing the name or description. When replacing the atlas, preserve its transparency, `1536 × 2288` dimensions, and v2 frame arrangement. Matching the dimensions alone does not make an arbitrary image a usable sprite atlas.

If you edit the repository files, copy them to the installation directory again and refresh the pet list. No configuration changes are needed to use the existing pack.

<a id="faq"></a>

## FAQ

### Why Is Young Handsome Missing from the Pet List?

Check that the files are under the `CODEX_HOME` used by your client (by default, `.codex` in your user directory), without an extra nested folder. Confirm that `pet.json` and the atlas are in the same directory, then refresh the list or restart the client. If there is no Pets settings page, check that your client supports the feature and your workspace allows pets.

### Why Does the Pet Image Fail to Load?

Check that `spritesheet.webp` was copied completely and that `spritesheetPath` in `pet.json` matches its filename. Use a client that supports the v2 pet format, and preserve the atlas's original dimensions and format.

### Why Is the Pet Not Animating?

Animation depends on the client state; an idle pet may not continuously show noticeable movement. According to the official documentation, pets use a still frame when the operating system's reduced motion setting is enabled. Check your system animation settings and confirm that the atlas has not been modified.

### Do I Need to Run an EXE or Startup Script?

No. This repository is a character asset pack loaded by the Codex desktop app. It contains no standalone executable or startup script. The host application needs to be running to use the pet.

<a id="contributing"></a>

## Contributing and Acknowledgments

Contributions to the character assets, instructions, and English translation are welcome:

- [Open an issue](https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet/issues): include your operating system, client version, reproduction steps, and relevant screenshots when reporting a problem.
- [Submit a pull request](https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet/pulls): describe your changes, keep both language versions in sync for documentation updates, and include a preview for atlas changes.

The README structure was inspired by [TonyNa-code/desktop-pet](https://github.com/TonyNa-code/desktop-pet/blob/main/README.md). Pet usage instructions reference the [official OpenAI pets documentation](https://learn.chatgpt.com/docs/pets).

## License

This repository includes an [MIT License](LICENSE). Rights to reference photography and any third-party materials belong to their respective rights holders; the repository's MIT license does not establish additional permission to use those materials.
