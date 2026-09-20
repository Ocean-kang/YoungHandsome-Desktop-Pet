# Young Handsome Desktop Pet 🏀

**让篮球少年 Young Handsome，陪你一起写代码。**

**简体中文** | [English](README.en.md)

![Codex Pet](https://img.shields.io/badge/Codex-Pet-222222) ![Sprite Format v2](https://img.shields.io/badge/Sprite_Format-v2-blue) ![WebP](https://img.shields.io/badge/Atlas-WebP-green)

Young Handsome 是用于 **Codex 桌面端**的篮球主题宠物角色包，包含角色配置与动画图集。将它安装到本地宠物目录后，即可在支持自定义宠物的桌面端中选择使用。

[效果预览](#preview) · [快速开始](#quick-start) · [自定义](#customization) · [常见问题](#faq) · [参与贡献](#contributing)

<a id="preview"></a>

## 效果预览

![Young Handsome 在桌面上的展示效果](screenshots/demo.png)

篮球球衣、Q 版人物，让你的桌面多一位运动伙伴。

[查看角色参考图片](assets/YoungHandsome.jpg)

## 角色特点

- **篮球主题形象**：以 Young Handsome 参考图为基础的 Q 版角色。
- **透明动画图集**：使用 WebP 资源，图集尺寸为 `1536 × 2288`。
- **v2 宠物格式**：配置采用 `spriteVersionNumber: 2`，图集为 8 列 × 11 行，每格 `192 × 208`。
- **本地安装**：角色包由一个 JSON 配置文件和一张 WebP 图集组成，无需为本仓库安装 Node.js、Python 或构建依赖。

本仓库提供角色外观与动画资源。桌面悬浮、拖动、显示与隐藏、任务状态等交互由宿主应用提供，实际表现取决于所用客户端版本及设置。

<a id="quick-start"></a>

## 快速开始

### 1. 准备桌面端并下载资源

请先安装支持自定义宠物和 v2 图集的 Codex 桌面端。以下以 Windows 为例；宠物设置与显示入口可参考 [OpenAI 官方宠物文档](https://learn.chatgpt.com/docs/pets)。官方文档中的桌面端产品名称和菜单措辞可能与当前安装版本有所不同。

在本仓库页面选择 **Code → Download ZIP**，解压下载的文件；也可以使用 Git：

```powershell
git clone https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet.git
cd YoungHandsome-Desktop-Pet
```

### 2. 安装角色包

**手动复制**

1. 在文件资源管理器地址栏输入 `%USERPROFILE%\.codex`。如果已设置 `CODEX_HOME`，请改为打开该环境变量指向的目录。
2. 在其中创建 `pets\young-handsome` 文件夹；缺少的上级目录也需要创建。
3. 将下载仓库中 `character` 文件夹里的 **`pet.json` 和 `spritesheet.webp`** 一起复制到 `young-handsome` 中。

默认安装后的目录应为：

```text
%USERPROFILE%\.codex\pets\young-handsome\
├── pet.json
└── spritesheet.webp
```

两个文件必须同级，不要在 `young-handsome` 中再嵌套一层 `character`。设置了 `CODEX_HOME` 时，目标目录为 `<CODEX_HOME>\pets\young-handsome\`。

**或使用 PowerShell**

在下载或克隆后的**仓库根目录**打开 PowerShell，执行以下命令。命令优先使用 `CODEX_HOME`；未设置时使用用户目录下的 `.codex`。再次执行会更新同名角色包的这两个文件。

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

### 3. 选择并显示宠物

1. 打开桌面端的 **设置 → 宠物（Settings → Pets）**。
2. 选择 **刷新（Refresh）**，然后选择 **Young Handsome**。
3. 在聊天输入框中输入 `/pet`，或在命令菜单中选择 **显示宠物（Show pet）**。

如果列表尚未更新，可重启桌面端后重新检查。完成后，Young Handsome 就可以出现在你的桌面上了。

## 资源结构

```text
YoungHandsome-Desktop-Pet/
├── assets/
│   └── YoungHandsome.jpg    # 角色参考图片
├── character/
│   ├── pet.json             # 角色配置
│   └── spritesheet.webp     # v2 动画图集
├── screenshots/
│   └── demo.png             # 桌面效果截图
├── .gitignore
├── LICENSE
├── README.md                # 中文说明（默认）
└── README.en.md             # 英文说明
```

安装时只需要 `character` 中的两个文件；参考图片和截图用于项目展示。

<a id="customization"></a>

## 自定义说明

角色配置位于 [`character/pet.json`](character/pet.json)：

| 字段 | 当前值 | 用途 |
| --- | --- | --- |
| `id` | `young-handsome` | 角色标识；制作独立变体时使用新的标识，并为其建立同名安装文件夹 |
| `displayName` | `Young Handsome` | 宠物选择器中的显示名称 |
| `description` | 英文角色简介 | 描述角色的主题和形象 |
| `spriteVersionNumber` | `2` | 图集格式版本，需与图集布局匹配 |
| `spritesheetPath` | `spritesheet.webp` | 相对于 `pet.json` 的图集路径 |

修改名称或描述时，保持 JSON 语法有效。替换图集时，保留透明背景、`1536 × 2288` 尺寸和 v2 的帧排列；保持相同尺寸并不代表任意图片都能作为动画图集使用。

若修改的是仓库中的文件，需要重新复制到安装目录，再刷新宠物列表。仅使用现有角色包无需修改配置。

<a id="faq"></a>

## 常见问题

### 安装后找不到 Young Handsome？

检查文件是否位于实际使用的 `CODEX_HOME`（默认为用户目录下的 `.codex`），以及是否多嵌套了一层目录。确认 `pet.json` 与图集同级，然后刷新宠物列表或重启客户端。若没有宠物设置入口，请检查客户端是否支持此功能，以及所在工作区是否允许使用宠物。

### 宠物图片无法显示？

确认 `spritesheet.webp` 已完整复制，且 `pet.json` 中的 `spritesheetPath` 与文件名一致。请使用支持 v2 宠物格式的客户端，并保留图集原始尺寸与格式。

### 宠物为什么没有播放动画？

动画表现取决于客户端状态；静止时不一定持续播放明显动作。根据官方文档，系统启用“减少动态效果”时，宠物会使用静态帧。可以检查系统动画设置，并确认图集未被修改。

### 需要运行 EXE 或启动脚本吗？

不需要。本仓库是由 Codex 桌面端加载的角色资源包，没有独立的可执行程序或启动脚本。使用时需要运行宿主应用。

<a id="contributing"></a>

## 贡献与致谢

欢迎改进角色资源、使用说明和英文翻译：

- [提交 Issue](https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet/issues)：反馈问题时，请附上系统、客户端版本、复现步骤及相关截图。
- [提交 Pull Request](https://github.com/Ocean-kang/YoungHandsome-Desktop-Pet/pulls)：说明修改内容；文档变更请同步中英文版本，图集变更请附上效果预览。

README 的章节组织参考了 [TonyNa-code/desktop-pet](https://github.com/TonyNa-code/desktop-pet/blob/main/README.md)。宠物使用方式参考 [OpenAI 官方宠物文档](https://learn.chatgpt.com/docs/pets)。

## 许可证

本仓库附有 [MIT License](LICENSE)。参考照片及可能涉及的第三方素材，其权利归相应权利人所有；仓库中的 MIT 许可证不代表已取得这些素材的额外授权。
