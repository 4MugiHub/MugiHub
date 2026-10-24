<p align="center">
  <img src="https://www.dropbox.com/scl/fi/8ibmsfo2fdrdva1qs2c3t/file_000000000e048207a242d5a33a95eb81.png?rlkey=qt2nowmuscezyc98he2ks8gnv&st=j9bfpdp1&raw=1" alt="MugiHub" width="720">
</p>

<div align="center">

# MugiHub

**A compact black-and-white UI library for Roblox script hubs, with a built-in SVG icon pack.**

Monochrome gradient theme · Animated glowing border · SVG icons everywhere · Any image link · Window background · Customizable bubble · Popup color picker · HWID/account configs · Optional webhook · Zero dependencies

[![Lua](https://img.shields.io/badge/Lua-Luau-2C2D72?style=for-the-badge&logo=lua&logoColor=white)](https://luau-lang.org/)
[![Roblox](https://img.shields.io/badge/Platform-Roblox-000000?style=for-the-badge&logo=roblox&logoColor=white)](https://www.roblox.com/)
[![Icons](https://img.shields.io/badge/Icons-428-ffffff?style=for-the-badge&labelColor=000000)](#icon-gallery)
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)](#license)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Library Info](#library-info)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Window API](#window-api)
- [Icons](#icons)
- [Images and Links](#images-and-links)
- [Window Background](#window-background)
- [Bubble (Minimize Button)](#bubble-minimize-button)
- [Tags API](#tags-api)
- [Tab and Section API](#tab-and-section-api)
- [Components](#components)
  - [Button](#button)
  - [Toggle](#toggle)
  - [Slider](#slider)
  - [Input](#input)
  - [Dropdown](#dropdown)
  - [Keybind](#keybind)
  - [Color Picker](#color-picker)
  - [Label / Progress / Paragraph / Separator / Line / Social / Copy Group / ReadMe](#label--progress--paragraph--separator--line--social--copy-group--readme)
  - [Flags](#flags)
- [Configs (HWID + Account)](#configs-hwid--account)
  - [The easy way: one component](#the-easy-way-one-component)
  - [How HWID and account work](#how-hwid-and-account-work)
  - [Files](#files)
  - [Performance](#performance)
  - [API (without the component)](#api-without-the-component)
- [Key System](#key-system)
  - [What It Provides](#what-it-provides)
  - [Requirements and Platform Notes](#requirements-and-platform-notes)
  - [Configuration Structure](#configuration-structure)
  - [General Options](#general-options)
  - [Window Options](#window-options)
  - [Appearance Options](#appearance-options)
  - [Authentication Options](#authentication-options)
  - [API Mode](#api-mode)
  - [Password Mode](#password-mode)
  - [Mode Switching](#mode-switching)
  - [Discord Support](#discord-support)
  - [Account and Device Policy](#account-and-device-policy)
  - [Behavior Options](#behavior-options)
  - [Callbacks](#callbacks)
  - [Controller Methods](#controller-methods)
  - [States, Feedback and Responsiveness](#states-feedback-and-responsiveness)
  - [Lifecycle and Cleanup](#lifecycle-and-cleanup)
  - [Security Model and Known Limitations](#security-model-and-known-limitations)
- [Color Picker Popup](#color-picker-popup)
- [Notifications](#notifications)
- [Search](#search)
- [Webhook (Optional)](#webhook-optional)
  - [What the Library Provides](#what-the-library-provides)
  - [Creating a Config](#creating-a-config)
  - [Multiple Configs](#multiple-configs)
  - [Registering Your Own Events](#registering-your-own-events)
  - [Sending Events](#sending-events)
  - [Custom Embeds](#custom-embeds)
  - [Attaching to Notifications](#attaching-to-notifications)
  - [Local Listeners](#local-listeners)
  - [Stats & Maintenance](#stats--maintenance)
  - [Full Method Reference](#full-method-reference)
  - [Any HTTP Endpoint Works](#any-http-endpoint-works)
  - [Security Note](#security-note)
- [Full Example](#full-example)
- [Icon Pack](#icon-pack)
- [Icon Gallery](#icon-gallery)
  - [Navigation (34)](#navigation-34)
  - [Actions (43)](#actions-43)
  - [Files (34)](#files-34)
  - [System (36)](#system-36)
  - [Settings (18)](#settings-18)
  - [Security (22)](#security-22)
  - [Status (25)](#status-25)
  - [Media (23)](#media-23)
  - [Social (21)](#social-21)
  - [Finance (23)](#finance-23)
  - [Nature (28)](#nature-28)
  - [Gaming (30)](#gaming-30)
  - [Roblox Ui (37)](#roblox-ui-37)
  - [Developer Tools (28)](#developer-tools-28)
  - [Transportation (26)](#transportation-26)
- [Validation Report](#validation-report)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

MugiHub is a single-file Luau UI library for building script hub interfaces on Roblox. It ships with a searchable sidebar, a draggable window, a customizable minimize bubble, stacked notifications, a full set of ready-made components, a popup color picker, a config manager and an **optional** webhook layer.

Roblox cannot render `.svg` files, so the library carries its own icon engine: every icon is stored as compact path data inside `Mugi` and rasterized at runtime into small anti-aliased PNGs (3x supersampled, cached in `MugiHub/Cache/`) so edges stay smooth, and tinted to follow the UI colors. If the executor cannot write files or load custom assets, icons automatically fall back to rounded frames. No emoji and no font glyphs are used for icons anywhere.

No external dependencies. No build step. Just `loadstring` one URL.

## Library Info

| | |
|---|---|
| **File** | `Mugi` (loadstring) / `Mugi.lua` (same content) |
| **Language** | Luau |
| **Style** | Monochrome (black and white gradient), no pink, compact |
| **Icons** | 428 built in, 3 variants as `.svg` files in [`icons/`](icons) |
| **Exports** | `MugiHub.Library`, `MugiHub.Webhook` |
| **Executor functions used (all optional)** | `request`/`http_request`, `writefile`, `readfile`, `isfile`, `listfiles`, `delfile`, `makefolder`, `isfolder`, `getcustomasset`, `gethui`, `gethwid`, `setclipboard` |

Everything that depends on an executor function degrades quietly: if a function is missing the feature is skipped, never an error.

## Features

- **Draggable window** with a minimize bubble you can fully customize (icon name, SVG, or any image link)
- **Compact black + white gradient look** inspired by Rayfield Gen 2: section cards, white accents, no pink
- **Animated border** - a white gradient runs around the window edge while the stroke softly fades
- **Red rounded-square close button** with a clean X, plus minimize button and confirmation dialog
- **SVG icons only** for tabs, tags, buttons, notifications, search, dropdowns and the bubble
- **Any image link** for the window icon, bubble, tab icons and background (Dropbox, Google Drive, Imgur, GitHub, Pinterest pages, any URL that returns an image) - `rbxassetid` is optional
- **Custom window background** from any link, with transparency, dim and fit controls
- **Tags with icons** (static, dynamic and executor tags)
- **Buttons with a mouse-pointer icon** instead of an arrow, so they are never mistaken for dropdowns
- **Modern dropdown** with filter, multi-select, live `Refresh`, and an optional per-row **delete button**
- **Popup color picker** with saturation/brightness box, hue bar, hex, RGB, presets and cancel/done
- **Key System** - a ready-made verification window with API mode (provider links and your own verification), password mode, Discord support, device and account policy, and callbacks
- **Config manager** - name input, save, deletable dropdown of saved configs, load, auto load, auto save
- **Configs follow the device OR the account** - the same config stays available if either the HWID or the Roblox account changes
- **Global search**, **stacked notifications**, **ripple click**, and an **optional webhook**

## Installation

```lua
local MugiHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()
```

- `MugiHub.Library` - the UI library
- `MugiHub.Webhook` - the optional webhook manager

> If you see `attempt to call a nil value` right after this line, it is almost always a stale GitHub raw cache. Wait about a minute and run again.

## Quick Start

```lua
local MugiHub = loadstring(game:HttpGet("URL_HERE"))()

local Window = MugiHub.Library:CreateWindow({
    "My Script",
    "A short tagline",
    105,
    UDim2.fromOffset(480, 275),
    Enum.KeyCode.RightControl,
    "hub",
})

local Tab = Window:AddTab({"Main", "home"})
local Section = Tab:AddSection("General")

Section:AddToggle({
    "Example Toggle",
    false,
    function(value) print("Toggle is now:", value) end
})

Section:AddConfigManager({})

MugiHub.Library:SetNotification({Type = "success", Content = "Loaded!", Delay = 3})
```

## Window API

```lua
local Window = MugiHub.Library:CreateWindow({
    "Window Title",             -- [1] Title
    "Subtitle text",            -- [2] Description
    105,                        -- [3] Tab width (pixels)
    UDim2.fromOffset(480, 275), -- [4] Size
    Enum.KeyCode.RightControl,  -- [5] Show/hide keybind
    "hub",                      -- [6] Icon: name, svg, asset id or any image link ("" to disable)
    {"TAG1", {"TAG2", "bolt"}}  -- [7] Tags (max 3), each text or {text, icon}
})
```

Named fields can be used instead of (or together with) positions:

| Field | Meaning |
|---|---|
| `Title`, `Description`, `Icon`, `Keybind`, `SizeUi`, `["Tab Width"]`, `Tags` | Same as the positional values |
| `Scale` | Window scale, default `0.9`, auto-fits small screens |
| `Background` | Background image link (see [Window Background](#window-background)) |
| `BackgroundTransparency` | Image transparency, default `0.35` |
| `BackgroundDim` | Black overlay transparency, default `0.45` |
| `BackgroundFit` | `"crop"` (default), `"fit"` or `"stretch"` |
| `Bubble` | Bubble icon: a string or `{Icon, Size, Position}` (see [Bubble](#bubble-minimize-button)) |

| Method | Description |
|---|---|
| `Window:SetTitle(text)` / `SetDescription(text)` | Update the header text |
| `Window:SetIcon(source)` | Change the header icon (name, svg, asset id or link; `nil` hides it) |
| `Window:SetBackground(source, {Fit, Transparency, Dim})` | Set or replace the background image |
| `Window:ClearBackground()` | Remove the background |
| `Window:SetBackgroundTransparency(n)` | Change background image transparency |
| `Window:SetBubbleIcon(source)` | Change the bubble icon at runtime |
| `Window:ColorPicker({Title, Color, Callback, OnDone, OnCancel})` | Open the popup color picker without a component |
| `Window:AddTab({name, icon})` | Create a tab |
| `Window:AddTabDivider(text)` | Group label between tabs |
| `Window:SelectTab(nameOrIndex)` | Switch tab from code |
| `Window:Toggle()` / `Window:SetOpen(bool)` | Show, hide or minimize |
| `Window:SetScale(0.5 - 1.5)` | Resize the whole window |
| `Window:Dialog({Title, Content, Buttons})` | Modal dialog; `Buttons = {{"Cancel"}, {"OK", callback, isDanger}}` |
| `Window:Destroy()` | Close and clean up everything |

When the window is closed, `MugiHub.Library.Unloaded` becomes `true`:

```lua
while not MugiHub.Library.Unloaded do task.wait(0.5) end
```

## Icons

Everywhere an icon is accepted you can pass **any** of these:

| Source | Example |
|---|---|
| Built-in name | `"sword"`, `"settings"`, `"shield-check"` |
| Alias (old short names still work) | `"combat"` -> `swords`, `"esp"` -> `eye`, `"gear"` -> `settings`, `"auto"` -> `refresh-cw` |
| Raw SVG path data | `"svg:M4 4L20 20M20 4L4 20"` |
| Full SVG text | `"<svg viewBox='0 0 24 24'><circle cx='12' cy='12' r='8'/></svg>"` |
| Roblox asset | `"rbxassetid://123456"` or just `123456` |
| Any image link | `"https://www.dropbox.com/..."`, Google Drive, Imgur, GitHub, ... |

Unknown icon names are skipped silently - they never raise an error.

```lua
local Tab = Window:AddTab({"Combat", "sword"})            -- built-in
local Tab2 = Window:AddTab({"Mine", "https://i.imgur.com/abc.png"})  -- image link

MugiHub.Library:RegisterIcon("logo", "svg:M12 3L21 8V16L12 21L3 16V8Z")
Window:AddTab({"Custom", "logo"})

print(MugiHub.Library:HasIcon("sword"))   -- true
print(#MugiHub.Library:GetIcons())        -- number of registered names
```

The SVG parser understands `M L H V C S Q T A Z` (absolute and relative), `<path>`, `<circle>`, `<ellipse>`, `<line>`, `<polyline>`, `<polygon>` and `<rect>`. Icons are stroke icons (stroke width 1.75 on a 24x24 grid); fills are not drawn for custom SVG text.

## Images and Links

The window icon, bubble, tab icons and the background all accept links. The library will:

1. Convert share links into direct links (Dropbox `raw=1`, Google Drive `uc?export=download`, GitHub `blob` to `raw`, Imgur page to image).
2. Download the bytes with the executor's `request`, detect PNG/JPG/GIF/WEBP by magic bytes, and cache the file in `MugiHub/Cache/` (hash-named, reused on the next run).
3. If the link is an HTML page (Pinterest and similar), read its `og:image` / `twitter:image` and use that picture instead.
4. Turn the cached file into an image with `getcustomasset`.

If anything fails (no HTTP, blocked site, not an image) the image is simply not shown - **no error is thrown**. `MugiHub.Library:ClearImageCache()` removes cached files.

> Executors need `request` (or `http_request`), `writefile` and `getcustomasset` for links. `rbxassetid` always works without any of them.

## Window Background

```lua
local Window = MugiHub.Library:CreateWindow({
    Title = "My Script",
    Icon = "hub",
    Background = "https://www.dropbox.com/scl/fi/xxxx/bg.png?rlkey=yyyy&dl=0",
    BackgroundTransparency = 0.35,   -- image
    BackgroundDim = 0.45,            -- black overlay
    BackgroundFit = "crop",          -- crop | fit | stretch
})

Window:SetBackground("https://i.imgur.com/abc.png", {Fit = "fit", Transparency = 0.5, Dim = 0.5})
Window:ClearBackground()
```

Pass a Pinterest/page link and the library uses the page's preview image.

## Bubble (Minimize Button)

The round draggable button shown when the window is minimized.

```lua
-- from the window icon (default)
MugiHub.Library:CreateWindow({"Title", "", 105, UDim2.fromOffset(480, 275), Enum.KeyCode.RightControl, "sword"})

-- fully custom
MugiHub.Library:CreateWindow({
    Title = "Title",
    Bubble = { Icon = "https://i.imgur.com/abc.png", Size = 48, Position = UDim2.new(0.05, 0, 0.1, 0) },
})

Window:SetBubbleIcon("shield")      -- change at runtime
Window:SetBubbleIcon("rbxassetid://123")
```

It stays inside the screen while dragging and keeps its animated border.

## Tags API

Accessible via `Window.Tags`. Tags can carry an icon.

```lua
local tag = Window.Tags:Add("LIVE", "zap")      -- text, icon
tag:Set("UPDATED")
tag:SetIcon("check-circle")
tag:Remove()

Window.Tags:AddDynamic("Players", function()
    return #game:GetService("Players"):GetPlayers()
end, 2, "users")                                 -- label, function, refresh seconds, icon

Window.Tags:AddExecutorTag(5, "cpu")             -- refresh seconds, icon (default "cpu")
```

Up to 3 tags are shown.

## Tab and Section API

```lua
local Tab = Window:AddTab({"Tab Name", "home"})
local Section = Tab:AddSection("Section Title")
local Collapsed = Tab:AddSection({Name = "Advanced", Collapsed = true})
```

Clicking a section header collapses or expands it. `Section:SetOpen(bool)` and `Section:SetTitle(text)` do the same from code. Tab icons are SVG icons that turn white when the tab is active.

## Components

Every component is created through a `Section` object. Every returned component also has `SetVisible(bool)`, `Destroy()` and `.Frame`.

### Button

```lua
Section:AddButton({
    "Do Something",
    "Runs a callback on click",
    function() end
})

Section:AddButton({Name = "Fast", Icon = false, Callback = function() end})       -- no icon
Section:AddButton({Name = "Save", Icon = "save", Callback = function() end})      -- custom icon
```

Buttons show a **mouse-pointer** icon on the right (so they are not confused with dropdowns). `Icon` accepts any icon source, or `false` to hide it. The returned object has `SetText(text)` and `SetIcon(source)`.

### Toggle

```lua
local Toggle = Section:AddToggle({ "Feature", false, function(value) end })
Toggle.Set(true)
print(Toggle.Get())
```

### Slider

```lua
local Slider = Section:AddSlider({ "Intensity", 0, 100, 50, function(value) end })

Section:AddSlider({ Name = "Speed", Min = 0, Max = 1, Default = 0.5, Increment = 0.1, Suffix = "", Callback = function(v) end })
```

### Input

```lua
local Input = Section:AddInput({ "Message", "Placeholder...", "", function(value) end })
Input.Set("hello")
print(Input.Get())
```

`Numeric = true` restricts the box to numbers.

### Dropdown

```lua
local Dropdown = Section:AddDropdown({
    "Mode",
    {"Option A", "Option B", "Option C"},
    "Option A",
    function(selected) print(selected[1]) end
})

Dropdown.Set("Option B")
print(Dropdown.Get()[1])
Dropdown.Refresh({"New 1", "New 2"}, true)   -- keepSelection
Dropdown.Open() Dropdown.Close() Dropdown.Clear()

local Multi = Section:AddDropdown({
    Name = "Hitboxes", Options = {"Head", "Chest", "Arms", "Legs"}, Default = {"Head"},
    Multi = true, Max = 3,
    Callback = function(selected) print(table.concat(selected, ", ")) end
})
```

Extra options:

| Option | Meaning |
|---|---|
| `Deletable = true` | Every row gets a trash icon button |
| `OnDelete = function(name) ... end` | Called when a row is deleted; return `false` to cancel |
| `ConfirmDelete = true` | Default `true`: first click arms the button (turns red), second click within about 2 seconds deletes |
| `DeleteIcon = "trash"` | Icon of the delete button |
| `Empty = "Nothing here"` | Text shown when the list is empty |
| `Filter = true` | Force the filter box (it appears automatically above 7 options) |

Only dropdowns created with `Deletable = true` have delete buttons, so normal dropdowns stay clean.

### Keybind

```lua
Section:AddKeybind({ "Toggle Key", Enum.KeyCode.E, function(key) end })
Section:AddKeybind({ Name = "Panic", Default = Enum.KeyCode.X, OnPress = function() end, Callback = function(key) end })
```

### Color Picker

```lua
local Picker = Section:AddColorPicker({ "ESP Color", Color3.fromRGB(255, 255, 255), function(color) print(color) end })
Picker.Set("#33CCFF")        -- Color3, hex string or {r, g, b}
print(Picker.Get())
Picker.Open()                -- open the popup from code
```

See [Color Picker Popup](#color-picker-popup).

### Label / Progress / Paragraph / Separator / Line / Social / Copy Group / ReadMe

```lua
local Label = Section:AddLabel("Plain text") Label.Set("New text")
local Bar = Section:AddProgress({"Loading", 25}) Bar.Set(80)             -- name, default, max (default 100)
local P = Section:AddParagraph({"Note", "Wrapped explanatory text."}) P.Set("New content")
Section:AddSeparator({"Advanced"}) Section:AddSeparator()
Section:AddLine()
Section:AddSocial({"Join Discord", "https://discord.gg/example", "rbxassetid://..."})
Section:AddCopyGroup({"Server IP", "play.example.com"})
Section:AddReadMe({"Getting Started", "Click to expand for setup instructions."})
```

### Flags

Give a component a `Flag` to include it in configs (toggle, slider, input, dropdown, keybind, color picker):

```lua
Section:AddToggle({Name = "Auto Farm", Default = false, Flag = "AutoFarm", Callback = function() end})
print(MugiHub.Library.Flags.AutoFarm)   -- live value
```

## Configs (HWID + Account)

### The easy way: one component

```lua
local Tab = Window:AddTab({"Config", "settings"})
local Section = Tab:AddSection("Configs")
Section:AddConfigManager({})
```

This adds, in one block:

1. **Config name** - type a name
2. **Saved configs** - dropdown of your configs, each row with a **trash icon** delete button (click once to arm, again to delete)
3. **Save config**, **Load config**, **Refresh list**
4. **Auto load on start** - loads the chosen config when the script runs
5. **Auto save changes** - saves the chosen config shortly after any flagged component changes

Options: `Name`, `InputName`, `DropdownName`, `AutoLoad = false` (never auto load), `AutoLoadDelay` (seconds, default `1.2`, gives your UI time to build before loading).

### How HWID and account work

When you save, the config stores a **hashed** fingerprint of the current **device (HWID)** and the current **Roblox account (UserId)**. A config is visible and usable when **either** one matches:

| Situation | Config available? |
|---|---|
| Same device, same account | Yes |
| Different device, same account | Yes (the account matches) |
| Same device, different account | Yes (the device matches) |
| Different device and different account | No |

Saving again from the new device/account adds it to the list (up to 8 each), so the config keeps following you. Raw HWIDs and UserIds are never written to disk, only one-way hashes. If `gethwid` is not available, a stable client id is used instead.

### Files

| Path | Content |
|---|---|
| `MugiHub/Configs/<name>.json` | One config (hashed owners + flag values) |
| `MugiHub/Configs/_index.json` | Fast index so listing never reads every file |
| `MugiHub/Configs/_settings.json` | Auto load / auto save pointers |
| `MugiHub/Cache/` | Downloaded images |

Configs from older versions in `MugiHub/*.json` are copied into the new folder automatically the first time.

### Performance

- The list comes from an in-memory index; the disk is scanned once and in the background.
- Writes are debounced (index and settings) and auto save waits 1.5 seconds after the last change.
- Loading applies about 6 values per frame so the game never hitches.
- Auto save is armed only after the UI is built and the auto load finished, so it can never overwrite a config with half-built defaults.

### API (without the component)

```lua
local Library = MugiHub.Library
local ok, name = Library:SaveConfig("legit")        -- returns true, cleanedName
Library:LoadConfig("legit", function(done, result) print(done, result) end)
Library:DeleteConfig("legit")                       -- true on success
print(Library:GetConfigs())                         -- names visible to this device/account
Library:RescanConfigs(function() end, true)         -- force rescan, callback when finished
Library:SetAutoLoad("legit")  Library:SetAutoLoad(nil)
Library:SetAutoSave("legit")  Library:SetAutoSave(nil)
Library:LoadAutoConfig(function(done, result) end)
Library:OnConfigsChanged(function() end)            -- returns an object with :Disconnect()
Library:RefreshOwner()                              -- re-read HWID/account (rarely needed)
```

Config names are cleaned to letters, digits, spaces, `-`, `_` and `.` (other characters become `_`). `SaveConfig` returns `false, reason` on failure, e.g. no `writefile`, an invalid name or a config owned by someone else.

## Key System

MugiHub includes a ready-made Key System window. It is created through the **CreateKeySystem** method of the library object, works on its own (no main window is required first), and reports its result through callbacks so your script decides what to load after the key is accepted. It uses the same monochrome gradient look, animated border, rounded corners, SVG icons and notification system as the rest of the library.

The Key System is fully driven by one structured configuration table. Every option below is optional; anything you leave out falls back to the default shown in the tables. Nested groups are merged with their defaults, so you only need to provide the values you want to change.

### What It Provides

- A compact, responsive window with a title, a description, a key input, a Verify button, one Get Key button per enabled provider, a status line with a loading indicator, a Discord support line and a red rounded close button with an SVG X
- Two authentication methods that can be enabled separately or together: **API mode** (provider links plus your own verification) and **Password mode** (a password stored in your script, no external service)
- A modular provider system: each provider supplies its own link or key-fetching function and its own verification, and nothing is assumed to be shared between providers
- Status states (idle, loading, success, error, warning, info) plus notifications through the normal MugiHub notification system
- Timeouts, controlled retries, a cooldown after failures, protection against double submission, and clear messages for empty input, invalid keys, service errors, timeouts, missing configuration and clipboard failures
- Optional device and account policy settings, with account-independent keys and no device binding as the default
- Optional local key persistence with automatic re-verification
- Callbacks for success, failure, accepted key, rejected key, closing and key requests, and a controller object for driving the window from code

### Requirements and Platform Notes

- The window itself needs only the standard MugiHub environment.
- Copying links and the Discord invite needs an executor clipboard function (setclipboard or toclipboard). If neither exists, the configured clipboard fallback is used instead.
- API mode verification through the built-in URL verifier needs an HTTP function (request, http_request, syn.request or http.request). Without one, only GET requests can fall back to the game HTTP get function and POST requests fail with a service error.
- Key persistence needs the executor file functions (writefile, readfile, isfile). Deleting a saved key also needs delfile.
- Roblox does not give scripts an official way to open an external browser or to read a stable device identifier. The Key System therefore copies links for the user to open manually, and device identification is only possible through functions you supply or through an executor function you explicitly allow.
- The Key System has not been tested in a real Roblox client or executor. Behavior that depends on executor functions follows their documented behavior and may differ between executors.

### Configuration Structure

| Group | Purpose |
|---|---|
| Title, Description, Icon | Text and icon shown in the header |
| AccountIndependent, AllowMultipleAccounts, HWIDMode | Account and device policy (top level) |
| Window | Size, scale, position, border, backdrop, close button |
| Appearance | Colors, fonts, icon size and alignment, animations |
| Authentication | Methods, texts, messages, timeouts, retries, API providers, password |
| Discord | Support line and invite link |
| Device | How a device identifier may be obtained and disclosed |
| Account | Whether account information may be sent to the built-in URL verifier |
| Behavior | Close on success, clipboard fallback, notifications, persistence |
| Callbacks | Functions the Key System calls for each outcome |

### General Options

| Option | Default | Description |
|---|---|---|
| Title | Access Verification | Main heading of the window. Can be changed later with the SetTitle controller method. |
| Description | Verify your key to continue. | Line under the title. An empty text hides it. Can be changed with SetDescription. |
| Icon | key | Header icon. Accepts a built-in icon name, an alias, raw SVG path data, full SVG text, an asset id or any image link, exactly like every other MugiHub icon. If the name is unknown, the key icon is used. |

### Window Options

These options live in the Window group.

| Option | Default | Description |
|---|---|---|
| Width | 360 | Window width in pixels. Limited to a range of 240 to 640. The height is automatic and follows the content. |
| Scale | 1 | Preferred scale. The Key System never exceeds it, but lowers the scale automatically so the whole window fits inside 94 percent of the screen width and 90 percent of the screen height. The final scale stays between 0.4 and 1.5. |
| Position | Centered | A UDim2 position for the window center. Leave it out to center the window. |
| Padding | 14 | Inner padding in pixels. Limited to 6 to 32. |
| CornerRadius | 12 | Corner radius of the window in pixels. Limited to 0 to 28. |
| Border | true | Shows the animated gradient border. Set to false for no border. |
| BorderTransparency | 0.25 | Base transparency of the border stroke. |
| BackgroundTransparency | 0.02 | Transparency of the window background. |
| Backdrop | true | Dims the screen behind the window and blocks clicks to interface underneath. With false there is no dimming and no click blocking. |
| BackdropTransparency | 0.5 | Transparency of the dimming layer. Higher values are lighter. |
| CloseButton | true | Shows the red rounded close button with an SVG X in the top-right corner. |
| CloseBehavior | Destroy | What the close button does. See the close behavior list below. |
| DisplayOrder | 150 | Display order of the screen interface, so it sits above the main window. |

Close behavior values:
- **Destroy** plays the closing animation, then removes the whole interface and cleans up every connection.
- **Hide** hides the window and the backdrop but keeps everything alive. It can be shown again with the Show controller method.
- **Callback** only calls the OnClose callback and leaves the window open, so your own code decides what happens.

The close button never closes the window by accident while the user types, because it is a separate button, and the backdrop never closes the window when it is tapped.

### Appearance Options

These options live in the Appearance group. All color options expect a Color3 value; invalid values are ignored and the default is used.

| Option | Default | Used for |
|---|---|---|
| Background | Library gradient | Window background. Leave it out for the standard MugiHub gradient. Setting a color replaces the gradient with a solid color. |
| Panel | White (translucent) | Fill of the header icon box and the mode switch bar |
| Accent | White | Header icon tint, the selected pill of the mode switch, and the default tint of provider icons |
| Text | Light gray | Title, selected mode label and enabled provider button labels |
| SubText | Mid gray | Description, placeholders, idle status text, notices and inactive labels |
| Border | White | Strokes around the window, header icon box, mode switch, input field, link box and default provider buttons |
| Button | White | Fill of the Verify button. The soft white gradient is applied only while this stays at the default white. |
| ButtonText | Near black | Label and icon color on the Verify button |
| Secondary | White (translucent) | Fill of the Get Key buttons |
| Input | Near black | Fill of the key input and of the link box |
| InputText | Light gray | Text typed into the input |
| Success | White | Status icon and text for success |
| Error | Red | Status icon and text for errors |
| Warning | Light gray | Status icon and text for warnings |
| Info | Soft gray | Status icon and text for information |
| Font | Gotham | Font for body text. Must be a Roblox font enum value. |
| FontBold | Gotham Bold | Font for the title, buttons and labels. |
| IconSize | 16 | Size in pixels of the icons inside buttons. Limited to 10 to 32. |
| IconAlign | Left | Places button icons Left or Right of the button text. Applies to the Verify and Get Key buttons. |
| Animations | true | Turns window, hover, status and spinner animations on or off. |
| AnimationTime | 0.2 | Base animation duration in seconds. All animation durations are scaled relative to the default of 0.2. |
| ReducedMotion | false | When true, every animation is skipped: no entrance animation, no border rotation, no spinner rotation and instant state changes. The result is identical to turning Animations off. |

Icons keep their quality on different screens because they are rendered as smooth anti-aliased images at three times their display size. If the executor cannot create image files, icons automatically fall back to the vector frame renderer.

### Authentication Options

These options live in the Authentication group.

| Option | Default | Description |
|---|---|---|
| DefaultMode | API | Which method is selected first: API or Password. If the requested method is not enabled, the enabled one is selected. |
| Placeholder | Enter your key... | Placeholder of the input in API mode. |
| PasswordPlaceholder | Enter the password... | Placeholder of the input in Password mode. |
| VerifyText | Verify | Text of the Verify button. |
| GetKeyText | Get Key | Base text of the Get Key buttons. |
| LoadingText | Verifying... | Text shown on the Verify button and in the status line while a key is being checked. |
| GetKeyLoadingText | Preparing link... | Status text while a Get Key request is running. |
| SuccessText | Key verified. | Status and notification text after a key is accepted. |
| ModeLabels | Key and Password | Labels of the two pills in the mode switch. Provide a table with API and Password entries. |
| Timeout | 10 | Seconds before one verification or key request attempt is treated as timed out. Limited to 2 to 60. |
| Retry | Attempts 1, Delay 1.5 | Controlled retry policy. See the retry section below. |
| Cooldown | 1 | Seconds a user must wait after a failed attempt before verifying again. Limited to 0 to 30. |
| Trim | true | Removes leading and trailing spaces from the key before checking it. |
| MaxLength | 512 | Keys longer than this are rejected as invalid without any check. |
| ShowProviderName | true | When more than one provider is enabled, appends the provider name to the Get Key text, for example Get Key - Name. Providers with their own ButtonText ignore this. |
| Messages | See below | Every user-facing message. |
| API | See API mode | Settings for API mode. |
| Password | See Password mode | Settings for Password mode. |

Message options (inside Messages):

| Message | Default text | Shown when |
|---|---|---|
| Empty | Enter your key to continue. | The input is empty when Verify is pressed |
| Invalid | That key is not valid. | Every verifier rejected the key, the password did not match, or the key was too long |
| ApiError | Could not reach the verification service. | A verifier failed with an error or returned nothing, and retries were used up |
| Timeout | The request timed out. Try again. | The last failed attempt timed out |
| NotConfigured | Verification is not configured. | There is no verifier in API mode, or no password in Password mode |
| NoMethod | No authentication method is enabled. | Neither API mode nor Password mode is enabled |
| ProviderMissing | This provider has no link configured. | A Get Key button is pressed for a provider without a link or key function |
| Copied | Link copied. Finish the steps, then paste your key here. | A link was copied to the clipboard |
| ClipboardFailed | Clipboard is not available. Copy the link manually. | Copying failed or no clipboard function exists |
| DeviceUnavailable | A device identifier is required but unavailable. | Strict device mode could not obtain an identifier |
| KeyReceived | Key received. Press Verify to check it. | A key function returned a key that was placed in the input |
| Busy | Please wait for the current request. | Verify or Get Key is pressed while another request runs |
| Cooldown | Please wait a moment before trying again. | Verify is pressed during the cooldown after a failure |

### API Mode

API mode is enabled through the Enabled option of the API group (inside Authentication). It separates **getting** a key from **verifying** a key, because those are different steps with different requirements.

API group options:

| Option | Default | Description |
|---|---|---|
| Enabled | false | Turns API mode on. |
| Providers | Empty list | List of provider tables. Only enabled providers get a Get Key button. |
| Verify | None | A global verification function used for every key, before any provider verifier. |
| VerifyUrl | None | A global verification request description handled by the built-in URL verifier. |

**How verification works.** When the user presses Verify, the Key System collects every available verifier in a fixed order: the global Verify function, then the global VerifyUrl, then for each enabled provider in the order listed its own Verify function followed by its own VerifyUrl. Each verifier is tried in turn.

- If a verifier accepts the key, verification ends at once and the key is accepted.
- If a verifier rejects the key, the next verifier is tried, because the key may belong to a different provider.
- If a verifier fails with an error, returns nothing or times out, it is retried according to the retry policy, then the next verifier is tried.
- If no verifier accepted the key and at least one failed with an error or timeout, the user sees the service error or timeout message. If every verifier clearly rejected the key, the user sees the invalid key message.
- If there is no verifier at all, the user sees the not configured message. The Key System never reports success without a verifier saying so.

**Custom verification functions.** A verifier function receives the typed key and a context table, and reports one of three outcomes: accepted, rejected, or failed. Returning true accepts the key. Returning false rejects it. Returning nothing, or raising an error, counts as a failure and is eligible for retries. The function runs in its own thread with the configured timeout, so a function that never returns cannot freeze the window.

The context table contains: the key, the mode, a Policy table (AccountIndependent, AllowMultipleAccounts and HWIDMode), a Send table that says whether the device identifier and account details may be forwarded by the built-in URL verifier, the device identifier when one was obtained, the account user id and name only when AccountIndependent is false, and, for provider verifiers, a Provider table with the provider id, name and settings. Custom functions receive this information whenever the policy collects it; what a custom function does with it is the developer's responsibility.

#### Provider Options

Each entry in the Providers list supports:

| Option | Default | Description |
|---|---|---|
| Id | Preset name or provider plus position | Unique identifier, used by the RequestKey controller method and by callbacks. |
| Preset | None | Optional shortcut. Linkvertise and Jnkie are recognized and only fill in the display name. See the provider status section. |
| Name | Preset name or Id | Display name. |
| Enabled | true | Set to false to hide the provider without removing it. |
| Logo (alias Icon) | link icon | Logo shown next to the Get Key text. Accepts a built-in icon name, SVG path data, SVG text, an asset id or an image link. Official brand SVG files are not bundled; supply your own asset or link. |
| Url | None | A fixed link that Get Key copies to the clipboard. |
| GetKey | None | A function that produces the link or key at press time. Takes precedence over Url. |
| ButtonText | Derived from GetKeyText | Full text for this provider's button. |
| Accent | None | Color for this provider's icon tint and button stroke. Without it the library accent and a neutral stroke are used. |
| Verify | None | Provider-specific verification function. |
| VerifyUrl | None | Provider-specific request description for the built-in URL verifier. |
| Settings | None | Free-form table passed through to your functions inside the context. The Key System never reads or sends it. |
| Timeout | Authentication Timeout | Per-provider timeout in seconds for its functions. |

A provider counts as ready for Get Key when it has a Url or a GetKey function. A provider without either stays visible but dimmed and shows the provider missing message when pressed.

#### Get Key Buttons

Each enabled provider gets its own button. The provider logo sits directly next to the Get Key text (on the left by default, or on the right with IconAlign). Buttons only exist for enabled providers, and the whole group is hidden in Password mode or when no provider is enabled.

When a Get Key button is pressed:
1. The Key System refuses the request if another request is running or the window is closing.
2. A fixed Url is used immediately. A GetKey function runs in its own thread with the timeout and retry policy.
3. A function may return a link text, or a table with a link, a key or both. Link texts must begin with http:// or https://; anything else is treated as a failure.
4. A returned link is copied to the clipboard automatically, followed by a notification and a status message. The status is informational, never success: the Key System does not assume a copied link is a valid key and does not assume the user finished the provider's steps.
5. A returned key is placed in the input and the user is asked to press Verify. It is never auto-accepted.
6. If copying fails or no clipboard function exists, an error message is shown and the clipboard fallback runs.
7. The OnGetKey callback is called with the provider id and the link.

Clipboard fallback values (Behavior group):
- **Show** reveals a selectable text box under the input that contains the link, so it can be copied by hand (default).
- **Notify** appends the link to the status and notification message.
- **None** shows only the failure message.

The same fallback applies when copying the Discord invite fails.

#### Built-in URL Verifier

For servers you control, a verification request can be described without writing a function. Put a description table in VerifyUrl (global or per provider). The Key System sends the request, checks the response, and reports accepted, rejected or failed.

| Option | Default | Description |
|---|---|---|
| Url | Required | Address to call. Placeholders are filled in and URL-encoded. |
| Method | GET | HTTP method. |
| Headers | None | Table of header names and values. Placeholders are filled in and control characters are removed. |
| Body | None | Request body text, for example JSON. Placeholders are filled in and JSON-escaped. |
| SuccessBody | None | Text that must appear in the response body. |
| MatchMode | contains | With contains the text only needs to appear; with equals the whole trimmed body must match. |
| SuccessJson | None | A table with Field (a dotted path such as a nested field name) and Value (default true). The response must be JSON and the field must equal the value. |

Response handling:
- Status codes 200 to 299 are evaluated against SuccessBody and SuccessJson. If neither is set, any successful status accepts the key, so set at least one in practice.
- Status 0, 429 and 500 or above count as service failures and are retried.
- Any other status counts as a clear rejection.
- A body that cannot be decoded as JSON when SuccessJson is set counts as a failure.

Placeholders available in Url, Headers and Body: key, hwid, userid, username and multi. The key is always available. The device identifier is filled in only when the device mode collected one and Device SendToVerifyUrl is true. User id and username are filled in only when AccountIndependent is false and Account SendToVerifyUrl is true. Multi is the text true or false from AllowMultipleAccounts. Placeholders that are not allowed are replaced with empty text. Unknown placeholder names are left untouched.

#### Retry Policy

Retry has two options: Attempts (extra tries after a failure, default 1, limited to 0 to 5) and Delay (seconds between tries, default 1.5, limited to 0.2 to 15). Retries apply only to failures (errors, empty results, timeouts, service status codes), per verifier or per key request. A clear rejection is never retried. While any request runs, Verify and Get Key are blocked, and after a failed attempt the cooldown applies.

#### Provider Support Status

- **Linkvertise and Jnkie:** MugiHub includes the integration structure for them, but no verified, official integration. Searching for official developer documentation did not produce a documented client verification flow that can be implemented honestly, so the Key System does not invent endpoints, parameters or callbacks. The Preset option only sets the display name. A provider counts as working only when you supply its link and a verification path, either your own backend (through VerifyUrl or a Verify function) or another mechanism that the provider documents.
- **Redirect and callback flows:** If a provider uses redirects or server-side callbacks, the user opens the copied link in a browser, completes the steps, and receives a key. Your backend checks the key. The Key System cannot observe the browser flow.
- **Not configured:** A provider with no link, or API mode with no verifier, shows a not configured message. It never reports success.
- **Brand assets:** No third-party logos are bundled. Use your own SVG, asset id or image link.

### Password Mode

Password mode is enabled through the Enabled option of the Password group (inside Authentication). It needs no external service and works offline.

| Option | Default | Description |
|---|---|---|
| Enabled | false | Turns Password mode on. |
| Password | Empty | A password text, or a list of accepted password texts. Empty texts are ignored. |
| CaseSensitive | true | When false, the typed text and the password are compared in lower case. |

The user types the password and presses Verify. A match accepts it; anything else shows the invalid message. With no password configured, the not configured message is shown instead of accepting anything.

**Security limits:** A password stored inside a Luau script that runs on the user's machine can be extracted by anyone who can read the script or inspect memory. Password mode is only suitable for simple gating, private groups or casual access control. It must never be treated as authentication that protects server resources. When real security is required, verify through a trusted backend using API mode with your own verification endpoint.

### Mode Switching

- If only one method is enabled, the mode switch is hidden and that method is used.
- If both are enabled, a switch appears under the header. The input icon (key or lock), placeholder and Get Key buttons change with the mode. Get Key buttons are shown only in API mode.
- If neither is enabled, the window shows the no method message and every verification attempt fails with it.
- The SetMode controller method changes the mode from code and returns whether the mode is enabled.

### Discord Support

The Discord group controls the support line at the bottom of the window. By default it reads Need Support? followed by a blue Discord link with an icon.

| Option | Default | Description |
|---|---|---|
| Enabled | true | Shows the support line. |
| Text | Need Support? | Plain text before the link. An empty text hides it. |
| LinkText | Discord | Text of the clickable part. |
| Color | Discord-style blue | Color of the link text and icon. |
| Icon | message-circle | Icon next to the link text. Accepts any MugiHub icon source. Set to false to hide it. MugiHub has no bundled Discord logo; supply your own SVG or asset if you want the brand logo. |
| IconSize | 14 | Icon size in pixels. Limited to 8 to 24. |
| InviteURL | Empty | Invite link to copy. The invite is never hard-coded in the library. |
| CopiedMessage | Discord invite copied to clipboard. | Status and notification text after copying. |
| MissingMessage | The Discord invite has not been configured. | Shown when the invite is empty. |

The link brightens on hover and dims briefly while pressed. Pressing it copies the invite and shows a notification. If copying fails, the clipboard fallback runs. The invite is not validated.

### Account and Device Policy

These options are top-level options (not inside a group) and are designed so that the default works for everyone.

| Option | Default | Description |
|---|---|---|
| AccountIndependent | true | Validation does not depend on the Roblox username or user id. Nothing about the account is placed in the context or sent. Set to false to let your own verifiers receive the account. |
| AllowMultipleAccounts | true | Declares that one key may be used by several accounts. |
| HWIDMode | Disabled | Device policy: Disabled, Optional or Strict. |

**AccountIndependent and AllowMultipleAccounts.** Keys are never bound to an account by default. The client cannot enforce how many accounts use a key; AllowMultipleAccounts is a policy flag delivered to your verifiers (in the context Policy table) and to the built-in URL verifier as the multi placeholder. Enforcement must happen on your server.

**HWIDMode values:**
- **Disabled:** no device identifier is collected or checked. This is the default and prioritizes cross-account and cross-device compatibility.
- **Optional:** the Key System tries to obtain an identifier; if one is available it is added to the context, and verification continues normally if it is not.
- **Strict:** an identifier is required. If none can be obtained, verification stops before any request and reports the device unavailable message. The Key System does not register, store or compare devices itself. Real binding (registration, validation, reset and conflict handling) must be done by your trusted backend using the identifier.

**Where an identifier comes from.** Roblox provides no official, stable HWID API for ordinary scripts, and the Key System does not claim otherwise. It does not fingerprint the executor, the IP address or the device. An identifier is used only if you provide a Provider function in the Device group, or you set UseExecutorFunction to true to allow the executor's gethwid function. Executor functions are unofficial and behavior varies.

Device group options:

| Option | Default | Description |
|---|---|---|
| Provider | None | A function that returns the identifier text. Takes precedence. |
| UseExecutorFunction | false | Allows the executor function when no Provider is set. |
| SendToVerifyUrl | false | Allows the built-in URL verifier to place the identifier in requests through the hwid placeholder. Without it the placeholder is empty. |
| Notice | A device identifier is used for verification. | Disclosure text shown in the window whenever HWIDMode is not Disabled. |

Account group options:

| Option | Default | Description |
|---|---|---|
| SendToVerifyUrl | false | Allows the built-in URL verifier to place the user id and name in requests, only when AccountIndependent is false. |
| Notice | Your Roblox account is used for verification. | Disclosure text shown whenever AccountIndependent is false. |

Policy summary: nothing about the device or account is sent anywhere unless you opt in, and the window shows a disclosure line in the cases where it is. The flags that control sending apply only to the built-in URL verifier; code you write yourself decides what it does with the context.

### Behavior Options

| Option | Default | Description |
|---|---|---|
| CloseOnSuccess | true | Destroys the window after the success delay. |
| SuccessDelay | 0.9 | Seconds the success state stays visible before OnSuccess is called and the window closes. |
| ClipboardFallback | Show | Show, Notify or None. |
| Notifications | true | Turns notifications for outcomes on or off. The status line is always updated. |
| NotificationDelay | 3 | Seconds notifications stay visible. |
| ReplaceExisting | true | Creating a Key System destroys the previous one first, so duplicates never stack. |
| Persist | See below | Local key persistence. |

Persistence options (inside Persist):

| Option | Default | Description |
|---|---|---|
| Enabled | false | Saves an accepted key to a file and checks it again on the next start. |
| Name | Default | File name, cleaned with the same rules as config names. The file is stored in the MugiHub KeySystem folder. |
| Days | 0 | Number of days a saved key stays usable. Zero means it never expires. |
| AutoVerify | true | Fills the input with the saved key and verifies it automatically after the window appears. |

A key is saved only after it has been accepted. A saved key goes through exactly the same verification as a typed one, and if it is rejected the file is deleted. The file contains the key as plain text together with the mode and a timestamp, so anyone with access to the device files can read it. The ClearSaved controller method deletes it.

### Callbacks

Callbacks are provided in the Callbacks group. Each runs in its own thread inside a protected call, so an error in your function never breaks the window; it is reported as a warning in the output.

| Callback | Receives | When it runs |
|---|---|---|
| OnKeyAccepted | The key and an info table (mode, and provider id if applicable) | Immediately when verification succeeds |
| OnSuccess | The key and the info table | After the success delay, once. This is the place to load your script. Called even if the user closes the window during the delay. |
| OnKeyRejected | The key and a reason code | A key is clearly rejected (invalid, or too long) |
| OnFailure | A readable message and a reason code | Any failed attempt, including empty input, rejected keys, service errors, timeouts, missing configuration and unavailable device |
| OnClose | Nothing | The user presses the close button or the Close controller method is used. Not called when the window is destroyed by success or by code. |
| OnGetKey | Provider id and the link | A key request produced a link |

Reason codes for OnFailure and OnKeyRejected: empty, invalid, api_error, timeout, not_configured, no_method and device_unavailable. A provider with nothing to open reports not_configured.

### Controller Methods

The CreateKeySystem method returns a controller table.

| Member | Description |
|---|---|
| Destroy | Closes the window with its animation (or immediately when given true), disconnects every event, stops every animation and removes the interface. Safe to call more than once. |
| Close | Does what the close button does, according to CloseBehavior, and calls OnClose. |
| Show and Hide | Show or hide the window and backdrop without destroying it. |
| SetTitle and SetDescription | Change the header texts. |
| SetStatus | Shows a status of kind idle, loading, success, error, warning or info with a text. |
| SetMode and GetMode | Switch between API and Password, and read the current mode. |
| SetKey and GetInput | Put text in the input and read it. |
| Verify | Runs verification, optionally with a given key, exactly like pressing the button. |
| RequestKey | Runs the Get Key action for a provider id. Returns whether a request started. |
| IsVerified | Whether a key has been accepted. |
| ClearSaved | Deletes the saved key file. |
| IsDestroyed | Whether the window is closing or gone. |
| Frame and Gui | The main frame and the screen interface, for advanced adjustments. |

### States, Feedback and Responsiveness

- **Status line:** the icon and text change by kind. Loading shows a rotating SVG loader (still when motion is reduced), success, error, warning and info each have their own icon and color.
- **Buttons:** Verify and Get Key are disabled while a request runs, the Verify button swaps its icon for a spinner and its label for the loading text, and repeated presses are ignored. The input is locked during a request.
- **Input:** pressing the keyboard confirm key submits. The input border highlights on focus.
- **Touch:** buttons use tap-based activation with the standard ripple, and no important function depends on hover. On touch devices the window moves up to 30 percent of the screen height while the input is focused, so the on-screen keyboard does not cover it, and returns afterwards.
- **Layout:** the height adapts to the content (for example more providers, a longer description or a long message), and the scale shrinks automatically on small screens so nothing is cut off. Icons are sized in pixels and do not shift the layout.
- **Success is never faked:** the success state appears only after a verifier or the password check accepts the key.

### Lifecycle and Cleanup

- Only one Key System exists at a time unless ReplaceExisting is turned off.
- Destroying the window disconnects every event, cancels the border and spinner animations and removes the interface. Results of requests that finish after destruction are ignored, so callbacks cannot fire twice and nothing indexes a removed interface.
- Creating and destroying the Key System repeatedly leaves nothing behind.
- The interface does not reset on respawn.

### Security Model and Known Limitations

- The Key System runs on the client. Anything inside a client script, including passwords, keys, links and adapter logic, can be inspected or modified by a determined user. A client-side check can gate access politely; it cannot protect secrets.
- For real protection, keep the actual resource on a trusted server and release it only after your backend validates the key. Never place API secrets, private tokens or credentials in the script.
- A copied link is not a key, and a provider's page being opened is not completion. The Key System never treats either as success.
- Responses are not trusted blindly: the built-in verifier requires a successful status and the configured body or JSON match, and anything unexpected is reported as a failure or a rejection.
- No username, user id, device identifier, IP address or other information is collected or sent unless you configure it, and the window discloses it when it does. There are no hidden webhooks or hidden data collection.
- Limitations: there is no input masking or visibility toggle for the key field; there is no drop shadow option because MugiHub windows do not use one; the window cannot be dragged; the library cannot open a web browser; official Linkvertise or Jnkie verification is not implemented, as explained in the provider status section; and the whole Key System was not tested in a real Roblox client or executor.

## Color Picker Popup

Clicking a color row opens a popup centered in the window, over a dimmed backdrop:

- Saturation/brightness box and hue bar (mouse or touch)
- Hex field (`#RRGGBB` or `#RGB`) and R / G / B fields
- 8 preset colors
- Old vs new preview
- **Cancel** restores the previous color, **Done** (or the X, or clicking outside) keeps the new one

The callback fires live while you drag. It also works without a component:

```lua
Window:ColorPicker({
    Title = "Pick a color",
    Color = Color3.fromRGB(80, 160, 255),
    Callback = function(c) print("live", c) end,
    OnDone = function(c) print("final", c) end,
    OnCancel = function(c) print("cancelled", c) end,
})
```

## Notifications

```lua
MugiHub.Library:SetNotification({ Content = "Settings applied", Delay = 3, Time = 0.25 })
MugiHub.Library:SetNotification({ Title = "Update", Content = "Config saved", Delay = 4 })
MugiHub.Library:SetNotification({ Type = "success", Content = "Saved" })   -- success | error | warning | info
MugiHub.Library:SetNotification({ Content = "Custom icon", Icon = "bug" })
MugiHub.Library:SetNotification("A plain string works too")

local notif = MugiHub.Library:SetNotification({Content = "Loading...", Delay = 10})
notif:Close()
```

`Type` picks an SVG icon (check-circle, x-circle, alert-triangle, info); `Icon` overrides it with any icon source.

## Search

Every component registered through a section is searchable from the sidebar search box. Typing jumps to the matching tab, opens the section, scrolls it into view and highlights it.

---

## Webhook (Optional)

The webhook system is off by default and does nothing unless you create a config. It is designed for **you, the script author, to log events you choose to log** — it does not collect or send anything on its own.

### What the Library Provides

The library only supplies the mechanism:

- Sending a JSON payload to a URL
- Queueing and rate limiting so you never spam the endpoint
- Error handling (`pcall`-wrapped, never crashes your script)
- A way to attach player/game context to a message, if you opt in

**It ships with no pre-made event names, titles, or colors.** That part is entirely up to you — you register whatever events make sense for your script, with whatever text and color you want. This keeps the library generic and keeps you in control of what leaves the client.

### Creating a Config

```lua
local Log = MugiHub.Webhook:NewConfig("Log", {
    URL        = "https://discord.com/api/webhooks/ID/TOKEN",
    Enabled    = true,
    Username   = "My Script",
    AvatarURL  = "",
    SendPlayer = true,
    SendGame   = true,
    Timestamp  = true,
    RateDelay  = 2,
    QueueMax   = 50,
    Color      = 0xE6E6E6,
})
```

| Field | Default | Description |
|---|---|---|
| `URL` | `""` | Destination URL. Empty means the config never sends anything. |
| `Enabled` | `true` | Master on/off switch |
| `Username` | `"MugiHub"` | Display name shown as the sender |
| `AvatarURL` | `""` | Sender avatar URL |
| `SendPlayer` | `true` | Include Username, DisplayName, UserId, and an avatar link |
| `SendGame` | `true` | Include PlaceId, JobId, and executor name |
| `Timestamp` | `true` | Include a timestamp on every embed |
| `RateDelay` | `2` | Minimum seconds between requests |
| `QueueMax` | `50` | Maximum queued messages before new ones are dropped |
| `Color` | `0xE6E6E6` | Fallback embed color when an event has none |

`SendPlayer` and `SendGame` only ever include: Roblox username, display name, UserId, PlaceId, JobId, and the executor's name. Nothing else is collected — no passwords, cookies, tokens, or other client data.

### Multiple Configs

You can create as many independent configs as you need. Each has its own queue, rate limit, and event list — they never interfere with each other.

```lua
local ActivityLog = MugiHub.Webhook:NewConfig("ActivityLog", {
    URL = "https://discord.com/api/webhooks/AAA/BBB",
})

local ErrorLog = MugiHub.Webhook:NewConfig("ErrorLog", {
    URL   = "https://discord.com/api/webhooks/CCC/DDD",
    Color = 0xFF3333,
})
```

Retrieve a config you created earlier:

```lua
local ActivityLog = MugiHub.Webhook:Get("ActivityLog")
```

### Registering Your Own Events

The library has no built-in events. Register the ones your script needs:

```lua
Log:RegisterEvent("ButtonClicked", {
    title = "Button Clicked",
    color = 0xE6E6E6,
})

Log:RegisterEvent("ScriptLoaded", {
    title = "Script Loaded",
    color = 0x00FF99,
})
```

### Sending Events

```lua
Log:Send("ScriptLoaded")

Log:Send("ButtonClicked", {
    button = "Execute",
})
```

Sending an event that was never registered still works — it falls back to a plain title made from the event name and the config's default color.

### Custom Embeds

For a one-off message that doesn't need a registered event:

```lua
Log:SendEmbed({
    Title       = "Script Loaded",
    Description = "Everything initialized correctly.",
    Color       = 0xE6E6E6,
    Footer      = "My Script v1.0",
    Fields      = {
        { name = "Status", value = "Online", inline = true },
    },
})
```

Send several embeds in one request (Discord allows up to 10):

```lua
Log:SendEmbeds({
    { Title = "First",  Color = 0xE6E6E6 },
    { Title = "Second", Color = 0x99CCFF },
})
```

Plain text, no embed:

```lua
Log:SendContent("Hello from my script.")
```

Fully custom payload:

```lua
Log:SendRaw({
    username = "Custom",
    content  = "Raw payload example",
})
```

### Attaching to Notifications

Optionally forward every `SetNotification` call to a webhook automatically:

```lua
MugiHub.Webhook:AttachToLibrary(MugiHub.Library, "Log")
```

After this, every notification shown in the UI is also sent through the `Log` config, tagged with whatever event name you registered for it (or a plain fallback if you didn't).

### Local Listeners

Run a local function when an event fires, without sending anything externally:

```lua
Log:On("ButtonClicked", function(data)
    print("Button clicked:", data and data.button)
end)

Log:On("*", function(eventName, data)
    print("Event fired:", eventName)
end)
```

### Stats & Maintenance

```lua
local stats = Log:GetStats()
print(stats.sent, stats.failed, stats.queued, stats.dropped)

Log:Flush()      -- send everything queued, right now
Log:ClearQueue()  -- discard everything queued

Log:Configure({RateDelay = 3})
Log:SetEnabled(false)
Log:SetURL("https://new-url")
```

### Full Method Reference

| Method | Description |
|---|---|
| `MugiHub.Webhook:NewConfig(name, cfg)` | Create a new config, returns the config object |
| `MugiHub.Webhook:Get(name)` | Retrieve a config created earlier |
| `MugiHub.Webhook:AttachToLibrary(lib, config)` | Forward every notification to a config |
| `config:RegisterEvent(name, {title, color})` | Define a named event |
| `config:Send(event, data)` | Send a registered (or ad-hoc) event |
| `config:SendEmbed(tbl)` | Send one custom embed |
| `config:SendEmbeds(list)` | Send up to 10 embeds in one request |
| `config:SendRaw(payload)` | Send a fully custom JSON payload |
| `config:SendContent(text)` | Send plain text, no embed |
| `config:On(event, cb)` | Local listener, does not send anything |
| `config:Configure(cfg)` | Update config fields |
| `config:SetEnabled(bool)` | Toggle on/off |
| `config:SetURL(url)` | Change the destination URL |
| `config:Flush()` | Send everything currently queued |
| `config:ClearQueue()` | Discard everything currently queued |
| `config:GetStats()` | Returns `{sent, failed, queued, dropped}` |
| `config:GetPlayerInfo()` | Returns `{Username, DisplayName, UserId}` |
| `config:GetGameInfo()` | Returns `{PlaceId, JobId, Executor}` |

### Any HTTP Endpoint Works

`URL` accepts any endpoint that accepts a JSON POST body — it doesn't have to be Discord:

```lua
MugiHub.Webhook:NewConfig("Test", {URL = "https://webhook.site/your-id"})
MugiHub.Webhook:NewConfig("Custom", {URL = "https://your-server.com/api/log"})
```

The default payload shape matches Discord's webhook format (`username`, `embeds`, `content`). If your endpoint expects something different, use `:SendRaw()` with whatever structure it needs.

### Security Note

> The webhook URL lives in client-side Roblox code, which means anyone who dumps the script's memory can read it.
>
> For anything sensitive, route through your own backend instead of exposing the real endpoint directly:
> ```
> Roblox Script → Your Proxy Server → Discord Webhook
> ```
> The script only ever needs to know the proxy's URL.

---

---

## Full Example

```lua
local MugiHub = loadstring(game:HttpGet("URL_HERE"))()
local Library = MugiHub.Library

local Log = MugiHub.Webhook:NewConfig("Log", { URL = "https://discord.com/api/webhooks/ID/TOKEN" })
Log:RegisterEvent("ButtonClicked", {title = "Button Clicked", color = 0xE6E6E6})

local Window = Library:CreateWindow({
    Title = "My Script",
    Description = "v1.0",
    SizeUi = UDim2.fromOffset(480, 275),
    Keybind = Enum.KeyCode.RightControl,
    Icon = "https://i.imgur.com/abc.png",           -- or "hub", "rbxassetid://..."
    Background = "https://i.imgur.com/background.png",
    Bubble = { Icon = "shield", Size = 46 },
    Tags = { {"Beta", "flask"} },
})

Window.Tags:AddExecutorTag(5, "cpu")
MugiHub.Webhook:AttachToLibrary(Library, "Log")

local Main = Window:AddTab({"Main", "home"})
local Combat = Window:AddTab({"Combat", "sword"})
local Settings = Window:AddTab({"Settings", "settings"})

local General = Main:AddSection("General")
General:AddButton({"Execute", "Runs the script", function()
    Log:Send("ButtonClicked", {button = "Execute"})
    Library:SetNotification({Type = "success", Content = "Executed"})
end})
General:AddToggle({Name = "Auto Farm", Default = false, Flag = "AutoFarm", Callback = function(state) end})
General:AddColorPicker({Name = "ESP Color", Default = Color3.fromRGB(255, 255, 255), Flag = "EspColor", Callback = function(c) end})

local Sec = Combat:AddSection("Aim")
Sec:AddDropdown({Name = "Target", Options = {"Head", "Torso"}, Default = "Head", Flag = "Target", Callback = function(s) end})

local Cfg = Settings:AddSection("Configs")
Cfg:AddConfigManager({})

Library:SetNotification({Type = "info", Content = "Script loaded!", Delay = 3})
```

## Icon Pack

The same 428 icons that live inside `Mugi` are shipped as plain `.svg` files, so you can use them in documentation, websites or other tools.

```
icons/
  outline/<category>/<name>.svg    main style, stroke 1.75, round caps and joins
  filled/<category>/<name>.svg     solid version
  duotone/<category>/<name>.svg    outline plus soft tinted fill
  tiles/<name>.svg                 dark preview tiles used by the gallery below
  contact-sheet.png                every outline icon on one sheet
  manifest.json                    name, category and file paths of every icon
```

- `viewBox="0 0 24 24"`, `stroke="currentColor"`, smooth Bezier curves, round caps and joins, one consistent stroke width
- Consistent kebab-case names: `refresh-cw.svg`, `tools.svg`, `sword.svg`, `settings.svg`, `gamepad.svg`, `shield-check.svg`
- Categories: Navigation 34 · Actions 43 · Files 34 · System 36 · Settings 18 · Security 22 · Status 25 · Media 23 · Social 21 · Finance 23 · Nature 28 · Gaming 30 · Roblox Ui 37 · Developer Tools 28 · Transportation 26
- All icons are original drawings made for this project and released under the project license.

![Contact sheet](icons/contact-sheet.png)

## Icon Gallery

Every icon, grouped by category. The name under each tile is what you pass to `AddTab`, tags, buttons and the rest of the API.

### Navigation (34)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/home.svg" width="56" height="56" alt="home"><br><sub><code>home</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/menu.svg" width="56" height="56" alt="menu"><br><sub><code>menu</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/arrow-up.svg" width="56" height="56" alt="arrow-up"><br><sub><code>arrow-up</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/arrow-right.svg" width="56" height="56" alt="arrow-right"><br><sub><code>arrow-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/arrow-down.svg" width="56" height="56" alt="arrow-down"><br><sub><code>arrow-down</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/arrow-left.svg" width="56" height="56" alt="arrow-left"><br><sub><code>arrow-left</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/arrow-up-right.svg" width="56" height="56" alt="arrow-up-right"><br><sub><code>arrow-up-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/arrow-down-left.svg" width="56" height="56" alt="arrow-down-left"><br><sub><code>arrow-down-left</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevron-up.svg" width="56" height="56" alt="chevron-up"><br><sub><code>chevron-up</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevron-right.svg" width="56" height="56" alt="chevron-right"><br><sub><code>chevron-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevron-down.svg" width="56" height="56" alt="chevron-down"><br><sub><code>chevron-down</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevron-left.svg" width="56" height="56" alt="chevron-left"><br><sub><code>chevron-left</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/chevrons-up-down.svg" width="56" height="56" alt="chevrons-up-down"><br><sub><code>chevrons-up-down</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevrons-right.svg" width="56" height="56" alt="chevrons-right"><br><sub><code>chevrons-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/external-link.svg" width="56" height="56" alt="external-link"><br><sub><code>external-link</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/map-pin.svg" width="56" height="56" alt="map-pin"><br><sub><code>map-pin</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/compass.svg" width="56" height="56" alt="compass"><br><sub><code>compass</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/navigation.svg" width="56" height="56" alt="navigation"><br><sub><code>navigation</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/undo.svg" width="56" height="56" alt="undo"><br><sub><code>undo</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/redo.svg" width="56" height="56" alt="redo"><br><sub><code>redo</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/corner-down-right.svg" width="56" height="56" alt="corner-down-right"><br><sub><code>corner-down-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/more-horizontal.svg" width="56" height="56" alt="more-horizontal"><br><sub><code>more-horizontal</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/more-vertical.svg" width="56" height="56" alt="more-vertical"><br><sub><code>more-vertical</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/grid.svg" width="56" height="56" alt="grid"><br><sub><code>grid</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/list.svg" width="56" height="56" alt="list"><br><sub><code>list</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sidebar.svg" width="56" height="56" alt="sidebar"><br><sub><code>sidebar</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/expand.svg" width="56" height="56" alt="expand"><br><sub><code>expand</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shrink.svg" width="56" height="56" alt="shrink"><br><sub><code>shrink</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/locate.svg" width="56" height="56" alt="locate"><br><sub><code>locate</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/route.svg" width="56" height="56" alt="route"><br><sub><code>route</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/signpost.svg" width="56" height="56" alt="signpost"><br><sub><code>signpost</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/back-to-top.svg" width="56" height="56" alt="back-to-top"><br><sub><code>back-to-top</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/panel-bottom.svg" width="56" height="56" alt="panel-bottom"><br><sub><code>panel-bottom</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chevrons-left.svg" width="56" height="56" alt="chevrons-left"><br><sub><code>chevrons-left</code></sub></td>
<td></td>
<td></td>
</tr>
</table>

### Actions (43)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/plus.svg" width="56" height="56" alt="plus"><br><sub><code>plus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/minus.svg" width="56" height="56" alt="minus"><br><sub><code>minus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/x.svg" width="56" height="56" alt="x"><br><sub><code>x</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/check.svg" width="56" height="56" alt="check"><br><sub><code>check</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/copy.svg" width="56" height="56" alt="copy"><br><sub><code>copy</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/clipboard-paste.svg" width="56" height="56" alt="clipboard-paste"><br><sub><code>clipboard-paste</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/scissors.svg" width="56" height="56" alt="scissors"><br><sub><code>scissors</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/trash.svg" width="56" height="56" alt="trash"><br><sub><code>trash</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pencil.svg" width="56" height="56" alt="pencil"><br><sub><code>pencil</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/refresh-cw.svg" width="56" height="56" alt="refresh-cw"><br><sub><code>refresh-cw</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/refresh-ccw.svg" width="56" height="56" alt="refresh-ccw"><br><sub><code>refresh-ccw</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/rotate-cw.svg" width="56" height="56" alt="rotate-cw"><br><sub><code>rotate-cw</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/download.svg" width="56" height="56" alt="download"><br><sub><code>download</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/upload.svg" width="56" height="56" alt="upload"><br><sub><code>upload</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/share.svg" width="56" height="56" alt="share"><br><sub><code>share</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/share-nodes.svg" width="56" height="56" alt="share-nodes"><br><sub><code>share-nodes</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/link.svg" width="56" height="56" alt="link"><br><sub><code>link</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/unlink.svg" width="56" height="56" alt="unlink"><br><sub><code>unlink</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/search.svg" width="56" height="56" alt="search"><br><sub><code>search</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/zoom-in.svg" width="56" height="56" alt="zoom-in"><br><sub><code>zoom-in</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/zoom-out.svg" width="56" height="56" alt="zoom-out"><br><sub><code>zoom-out</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/filter.svg" width="56" height="56" alt="filter"><br><sub><code>filter</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sort.svg" width="56" height="56" alt="sort"><br><sub><code>sort</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/eye.svg" width="56" height="56" alt="eye"><br><sub><code>eye</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/eye-off.svg" width="56" height="56" alt="eye-off"><br><sub><code>eye-off</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/heart.svg" width="56" height="56" alt="heart"><br><sub><code>heart</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/star.svg" width="56" height="56" alt="star"><br><sub><code>star</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bookmark.svg" width="56" height="56" alt="bookmark"><br><sub><code>bookmark</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/flag.svg" width="56" height="56" alt="flag"><br><sub><code>flag</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pin.svg" width="56" height="56" alt="pin"><br><sub><code>pin</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/mouse-pointer.svg" width="56" height="56" alt="mouse-pointer"><br><sub><code>mouse-pointer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/mouse.svg" width="56" height="56" alt="mouse"><br><sub><code>mouse</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/hand.svg" width="56" height="56" alt="hand"><br><sub><code>hand</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/move.svg" width="56" height="56" alt="move"><br><sub><code>move</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/maximize.svg" width="56" height="56" alt="maximize"><br><sub><code>maximize</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/minimize.svg" width="56" height="56" alt="minimize"><br><sub><code>minimize</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/send.svg" width="56" height="56" alt="send"><br><sub><code>send</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/power.svg" width="56" height="56" alt="power"><br><sub><code>power</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/log-in.svg" width="56" height="56" alt="log-in"><br><sub><code>log-in</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/log-out.svg" width="56" height="56" alt="log-out"><br><sub><code>log-out</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/grip.svg" width="56" height="56" alt="grip"><br><sub><code>grip</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pointer-click.svg" width="56" height="56" alt="pointer-click"><br><sub><code>pointer-click</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/erase.svg" width="56" height="56" alt="erase"><br><sub><code>erase</code></sub></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>

### Files (34)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/file.svg" width="56" height="56" alt="file"><br><sub><code>file</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-text.svg" width="56" height="56" alt="file-text"><br><sub><code>file-text</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-plus.svg" width="56" height="56" alt="file-plus"><br><sub><code>file-plus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-minus.svg" width="56" height="56" alt="file-minus"><br><sub><code>file-minus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-check.svg" width="56" height="56" alt="file-check"><br><sub><code>file-check</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-code.svg" width="56" height="56" alt="file-code"><br><sub><code>file-code</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/file-image.svg" width="56" height="56" alt="file-image"><br><sub><code>file-image</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-audio.svg" width="56" height="56" alt="file-audio"><br><sub><code>file-audio</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-video.svg" width="56" height="56" alt="file-video"><br><sub><code>file-video</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-archive.svg" width="56" height="56" alt="file-archive"><br><sub><code>file-archive</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-lock.svg" width="56" height="56" alt="file-lock"><br><sub><code>file-lock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-search.svg" width="56" height="56" alt="file-search"><br><sub><code>file-search</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/file-json.svg" width="56" height="56" alt="file-json"><br><sub><code>file-json</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/folder.svg" width="56" height="56" alt="folder"><br><sub><code>folder</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/folder-open.svg" width="56" height="56" alt="folder-open"><br><sub><code>folder-open</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/folder-plus.svg" width="56" height="56" alt="folder-plus"><br><sub><code>folder-plus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/folder-lock.svg" width="56" height="56" alt="folder-lock"><br><sub><code>folder-lock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/folder-tree.svg" width="56" height="56" alt="folder-tree"><br><sub><code>folder-tree</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/save.svg" width="56" height="56" alt="save"><br><sub><code>save</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/clipboard.svg" width="56" height="56" alt="clipboard"><br><sub><code>clipboard</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/clipboard-check.svg" width="56" height="56" alt="clipboard-check"><br><sub><code>clipboard-check</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/notebook.svg" width="56" height="56" alt="notebook"><br><sub><code>notebook</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/book.svg" width="56" height="56" alt="book"><br><sub><code>book</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/book-open.svg" width="56" height="56" alt="book-open"><br><sub><code>book-open</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/archive.svg" width="56" height="56" alt="archive"><br><sub><code>archive</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/paperclip.svg" width="56" height="56" alt="paperclip"><br><sub><code>paperclip</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/image.svg" width="56" height="56" alt="image"><br><sub><code>image</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/images.svg" width="56" height="56" alt="images"><br><sub><code>images</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/file-spreadsheet.svg" width="56" height="56" alt="file-spreadsheet"><br><sub><code>file-spreadsheet</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/box.svg" width="56" height="56" alt="box"><br><sub><code>box</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/database-export.svg" width="56" height="56" alt="database-export"><br><sub><code>database-export</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-file.svg" width="56" height="56" alt="cloud-file"><br><sub><code>cloud-file</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/history.svg" width="56" height="56" alt="history"><br><sub><code>history</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/inbox.svg" width="56" height="56" alt="inbox"><br><sub><code>inbox</code></sub></td>
<td></td>
<td></td>
</tr>
</table>

### System (36)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/cpu.svg" width="56" height="56" alt="cpu"><br><sub><code>cpu</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/hard-drive.svg" width="56" height="56" alt="hard-drive"><br><sub><code>hard-drive</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/server.svg" width="56" height="56" alt="server"><br><sub><code>server</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/monitor.svg" width="56" height="56" alt="monitor"><br><sub><code>monitor</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/laptop.svg" width="56" height="56" alt="laptop"><br><sub><code>laptop</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/smartphone.svg" width="56" height="56" alt="smartphone"><br><sub><code>smartphone</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/tablet.svg" width="56" height="56" alt="tablet"><br><sub><code>tablet</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/keyboard.svg" width="56" height="56" alt="keyboard"><br><sub><code>keyboard</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/printer.svg" width="56" height="56" alt="printer"><br><sub><code>printer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/wifi.svg" width="56" height="56" alt="wifi"><br><sub><code>wifi</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/wifi-off.svg" width="56" height="56" alt="wifi-off"><br><sub><code>wifi-off</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bluetooth.svg" width="56" height="56" alt="bluetooth"><br><sub><code>bluetooth</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/battery.svg" width="56" height="56" alt="battery"><br><sub><code>battery</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/battery-charging.svg" width="56" height="56" alt="battery-charging"><br><sub><code>battery-charging</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/plug.svg" width="56" height="56" alt="plug"><br><sub><code>plug</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud.svg" width="56" height="56" alt="cloud"><br><sub><code>cloud</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-upload.svg" width="56" height="56" alt="cloud-upload"><br><sub><code>cloud-upload</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-download.svg" width="56" height="56" alt="cloud-download"><br><sub><code>cloud-download</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/globe.svg" width="56" height="56" alt="globe"><br><sub><code>globe</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/clock.svg" width="56" height="56" alt="clock"><br><sub><code>clock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/timer.svg" width="56" height="56" alt="timer"><br><sub><code>timer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/hourglass.svg" width="56" height="56" alt="hourglass"><br><sub><code>hourglass</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/calendar.svg" width="56" height="56" alt="calendar"><br><sub><code>calendar</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bell.svg" width="56" height="56" alt="bell"><br><sub><code>bell</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/bell-off.svg" width="56" height="56" alt="bell-off"><br><sub><code>bell-off</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/mail.svg" width="56" height="56" alt="mail"><br><sub><code>mail</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/headphones.svg" width="56" height="56" alt="headphones"><br><sub><code>headphones</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/usb.svg" width="56" height="56" alt="usb"><br><sub><code>usb</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/memory-card.svg" width="56" height="56" alt="memory-card"><br><sub><code>memory-card</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/power-plug-off.svg" width="56" height="56" alt="power-plug-off"><br><sub><code>power-plug-off</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/signal.svg" width="56" height="56" alt="signal"><br><sub><code>signal</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/airplane-mode.svg" width="56" height="56" alt="airplane-mode"><br><sub><code>airplane-mode</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/qr-code.svg" width="56" height="56" alt="qr-code"><br><sub><code>qr-code</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/disc.svg" width="56" height="56" alt="disc"><br><sub><code>disc</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/webcam.svg" width="56" height="56" alt="webcam"><br><sub><code>webcam</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/terminal-window.svg" width="56" height="56" alt="terminal-window"><br><sub><code>terminal-window</code></sub></td>
</tr>
</table>

### Settings (18)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/settings.svg" width="56" height="56" alt="settings"><br><sub><code>settings</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/settings-2.svg" width="56" height="56" alt="settings-2"><br><sub><code>settings-2</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sliders.svg" width="56" height="56" alt="sliders"><br><sub><code>sliders</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sliders-vertical.svg" width="56" height="56" alt="sliders-vertical"><br><sub><code>sliders-vertical</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/tools.svg" width="56" height="56" alt="tools"><br><sub><code>tools</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/wrench.svg" width="56" height="56" alt="wrench"><br><sub><code>wrench</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/hammer.svg" width="56" height="56" alt="hammer"><br><sub><code>hammer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/screwdriver.svg" width="56" height="56" alt="screwdriver"><br><sub><code>screwdriver</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/toggle-left.svg" width="56" height="56" alt="toggle-left"><br><sub><code>toggle-left</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/toggle-right.svg" width="56" height="56" alt="toggle-right"><br><sub><code>toggle-right</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/palette.svg" width="56" height="56" alt="palette"><br><sub><code>palette</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/paintbrush.svg" width="56" height="56" alt="paintbrush"><br><sub><code>paintbrush</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/wand.svg" width="56" height="56" alt="wand"><br><sub><code>wand</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/contrast.svg" width="56" height="56" alt="contrast"><br><sub><code>contrast</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/gauge.svg" width="56" height="56" alt="gauge"><br><sub><code>gauge</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/layers.svg" width="56" height="56" alt="layers"><br><sub><code>layers</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/adjustments.svg" width="56" height="56" alt="adjustments"><br><sub><code>adjustments</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ruler.svg" width="56" height="56" alt="ruler"><br><sub><code>ruler</code></sub></td>
</tr>
</table>

### Security (22)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/shield.svg" width="56" height="56" alt="shield"><br><sub><code>shield</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-check.svg" width="56" height="56" alt="shield-check"><br><sub><code>shield-check</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-alert.svg" width="56" height="56" alt="shield-alert"><br><sub><code>shield-alert</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-x.svg" width="56" height="56" alt="shield-x"><br><sub><code>shield-x</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-off.svg" width="56" height="56" alt="shield-off"><br><sub><code>shield-off</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-plus.svg" width="56" height="56" alt="shield-plus"><br><sub><code>shield-plus</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/shield-half.svg" width="56" height="56" alt="shield-half"><br><sub><code>shield-half</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/lock.svg" width="56" height="56" alt="lock"><br><sub><code>lock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/unlock.svg" width="56" height="56" alt="unlock"><br><sub><code>unlock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/key.svg" width="56" height="56" alt="key"><br><sub><code>key</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fingerprint.svg" width="56" height="56" alt="fingerprint"><br><sub><code>fingerprint</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bug.svg" width="56" height="56" alt="bug"><br><sub><code>bug</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/scan-eye.svg" width="56" height="56" alt="scan-eye"><br><sub><code>scan-eye</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/id-card.svg" width="56" height="56" alt="id-card"><br><sub><code>id-card</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/user-check.svg" width="56" height="56" alt="user-check"><br><sub><code>user-check</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/siren.svg" width="56" height="56" alt="siren"><br><sub><code>siren</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ban.svg" width="56" height="56" alt="ban"><br><sub><code>ban</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/badge-check.svg" width="56" height="56" alt="badge-check"><br><sub><code>badge-check</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/eye-lock.svg" width="56" height="56" alt="eye-lock"><br><sub><code>eye-lock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/password.svg" width="56" height="56" alt="password"><br><sub><code>password</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/firewall.svg" width="56" height="56" alt="firewall"><br><sub><code>firewall</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-lock.svg" width="56" height="56" alt="shield-lock"><br><sub><code>shield-lock</code></sub></td>
<td></td>
<td></td>
</tr>
</table>

### Status (25)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/check-circle.svg" width="56" height="56" alt="check-circle"><br><sub><code>check-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/x-circle.svg" width="56" height="56" alt="x-circle"><br><sub><code>x-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/alert-circle.svg" width="56" height="56" alt="alert-circle"><br><sub><code>alert-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/alert-triangle.svg" width="56" height="56" alt="alert-triangle"><br><sub><code>alert-triangle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/alert-octagon.svg" width="56" height="56" alt="alert-octagon"><br><sub><code>alert-octagon</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/info.svg" width="56" height="56" alt="info"><br><sub><code>info</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/help-circle.svg" width="56" height="56" alt="help-circle"><br><sub><code>help-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/loader.svg" width="56" height="56" alt="loader"><br><sub><code>loader</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/spinner.svg" width="56" height="56" alt="spinner"><br><sub><code>spinner</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/activity.svg" width="56" height="56" alt="activity"><br><sub><code>activity</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/heart-pulse.svg" width="56" height="56" alt="heart-pulse"><br><sub><code>heart-pulse</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/thumbs-up.svg" width="56" height="56" alt="thumbs-up"><br><sub><code>thumbs-up</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/thumbs-down.svg" width="56" height="56" alt="thumbs-down"><br><sub><code>thumbs-down</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bell-ring.svg" width="56" height="56" alt="bell-ring"><br><sub><code>bell-ring</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/circle-dot.svg" width="56" height="56" alt="circle-dot"><br><sub><code>circle-dot</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/verified.svg" width="56" height="56" alt="verified"><br><sub><code>verified</code><
