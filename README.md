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
<td align="center" width="16%"><img src="icons/tiles/verified.svg" width="56" height="56" alt="verified"><br><sub><code>verified</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/zap.svg" width="56" height="56" alt="zap"><br><sub><code>zap</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/progress.svg" width="56" height="56" alt="progress"><br><sub><code>progress</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/online.svg" width="56" height="56" alt="online"><br><sub><code>online</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/offline.svg" width="56" height="56" alt="offline"><br><sub><code>offline</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pause-circle.svg" width="56" height="56" alt="pause-circle"><br><sub><code>pause-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/stop-circle.svg" width="56" height="56" alt="stop-circle"><br><sub><code>stop-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/clock-alert.svg" width="56" height="56" alt="clock-alert"><br><sub><code>clock-alert</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/target-check.svg" width="56" height="56" alt="target-check"><br><sub><code>target-check</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/sparkle.svg" width="56" height="56" alt="sparkle"><br><sub><code>sparkle</code></sub></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>

### Media (23)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/play.svg" width="56" height="56" alt="play"><br><sub><code>play</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pause.svg" width="56" height="56" alt="pause"><br><sub><code>pause</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/stop.svg" width="56" height="56" alt="stop"><br><sub><code>stop</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/skip-forward.svg" width="56" height="56" alt="skip-forward"><br><sub><code>skip-forward</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/skip-back.svg" width="56" height="56" alt="skip-back"><br><sub><code>skip-back</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fast-forward.svg" width="56" height="56" alt="fast-forward"><br><sub><code>fast-forward</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/rewind.svg" width="56" height="56" alt="rewind"><br><sub><code>rewind</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/repeat.svg" width="56" height="56" alt="repeat"><br><sub><code>repeat</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shuffle.svg" width="56" height="56" alt="shuffle"><br><sub><code>shuffle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/volume.svg" width="56" height="56" alt="volume"><br><sub><code>volume</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/volume-low.svg" width="56" height="56" alt="volume-low"><br><sub><code>volume-low</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/volume-mute.svg" width="56" height="56" alt="volume-mute"><br><sub><code>volume-mute</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/mic.svg" width="56" height="56" alt="mic"><br><sub><code>mic</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/mic-off.svg" width="56" height="56" alt="mic-off"><br><sub><code>mic-off</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/camera.svg" width="56" height="56" alt="camera"><br><sub><code>camera</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/video.svg" width="56" height="56" alt="video"><br><sub><code>video</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/music.svg" width="56" height="56" alt="music"><br><sub><code>music</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/film.svg" width="56" height="56" alt="film"><br><sub><code>film</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/radio.svg" width="56" height="56" alt="radio"><br><sub><code>radio</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cast.svg" width="56" height="56" alt="cast"><br><sub><code>cast</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/subtitles.svg" width="56" height="56" alt="subtitles"><br><sub><code>subtitles</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/equalizer.svg" width="56" height="56" alt="equalizer"><br><sub><code>equalizer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/image-play.svg" width="56" height="56" alt="image-play"><br><sub><code>image-play</code></sub></td>
<td></td>
</tr>
</table>

### Social (21)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/user.svg" width="56" height="56" alt="user"><br><sub><code>user</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/users.svg" width="56" height="56" alt="users"><br><sub><code>users</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/user-plus.svg" width="56" height="56" alt="user-plus"><br><sub><code>user-plus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/user-minus.svg" width="56" height="56" alt="user-minus"><br><sub><code>user-minus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/user-circle.svg" width="56" height="56" alt="user-circle"><br><sub><code>user-circle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/message-circle.svg" width="56" height="56" alt="message-circle"><br><sub><code>message-circle</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/message-square.svg" width="56" height="56" alt="message-square"><br><sub><code>message-square</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chat-dots.svg" width="56" height="56" alt="chat-dots"><br><sub><code>chat-dots</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/smile.svg" width="56" height="56" alt="smile"><br><sub><code>smile</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/frown.svg" width="56" height="56" alt="frown"><br><sub><code>frown</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/meh.svg" width="56" height="56" alt="meh"><br><sub><code>meh</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/at-sign.svg" width="56" height="56" alt="at-sign"><br><sub><code>at-sign</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/hash.svg" width="56" height="56" alt="hash"><br><sub><code>hash</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/gift.svg" width="56" height="56" alt="gift"><br><sub><code>gift</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/megaphone.svg" width="56" height="56" alt="megaphone"><br><sub><code>megaphone</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/share-2.svg" width="56" height="56" alt="share-2"><br><sub><code>share-2</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/group.svg" width="56" height="56" alt="group"><br><sub><code>group</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/send-message.svg" width="56" height="56" alt="send-message"><br><sub><code>send-message</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/link-2.svg" width="56" height="56" alt="link-2"><br><sub><code>link-2</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/rss.svg" width="56" height="56" alt="rss"><br><sub><code>rss</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bookmark-check.svg" width="56" height="56" alt="bookmark-check"><br><sub><code>bookmark-check</code></sub></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>

### Finance (23)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/coins.svg" width="56" height="56" alt="coins"><br><sub><code>coins</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/wallet.svg" width="56" height="56" alt="wallet"><br><sub><code>wallet</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/credit-card.svg" width="56" height="56" alt="credit-card"><br><sub><code>credit-card</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/banknote.svg" width="56" height="56" alt="banknote"><br><sub><code>banknote</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/piggy-bank.svg" width="56" height="56" alt="piggy-bank"><br><sub><code>piggy-bank</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/receipt.svg" width="56" height="56" alt="receipt"><br><sub><code>receipt</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/shopping-cart.svg" width="56" height="56" alt="shopping-cart"><br><sub><code>shopping-cart</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shopping-bag.svg" width="56" height="56" alt="shopping-bag"><br><sub><code>shopping-bag</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/tag.svg" width="56" height="56" alt="tag"><br><sub><code>tag</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/percent.svg" width="56" height="56" alt="percent"><br><sub><code>percent</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/trending-up.svg" width="56" height="56" alt="trending-up"><br><sub><code>trending-up</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/trending-down.svg" width="56" height="56" alt="trending-down"><br><sub><code>trending-down</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/bar-chart.svg" width="56" height="56" alt="bar-chart"><br><sub><code>bar-chart</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/pie-chart.svg" width="56" height="56" alt="pie-chart"><br><sub><code>pie-chart</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/line-chart.svg" width="56" height="56" alt="line-chart"><br><sub><code>line-chart</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/calculator.svg" width="56" height="56" alt="calculator"><br><sub><code>calculator</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/store.svg" width="56" height="56" alt="store"><br><sub><code>store</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bank.svg" width="56" height="56" alt="bank"><br><sub><code>bank</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/dollar-sign.svg" width="56" height="56" alt="dollar-sign"><br><sub><code>dollar-sign</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/safe.svg" width="56" height="56" alt="safe"><br><sub><code>safe</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/scale.svg" width="56" height="56" alt="scale"><br><sub><code>scale</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/gem.svg" width="56" height="56" alt="gem"><br><sub><code>gem</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/badge-dollar.svg" width="56" height="56" alt="badge-dollar"><br><sub><code>badge-dollar</code></sub></td>
<td></td>
</tr>
</table>

### Nature (28)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/sun.svg" width="56" height="56" alt="sun"><br><sub><code>sun</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/moon.svg" width="56" height="56" alt="moon"><br><sub><code>moon</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sunrise.svg" width="56" height="56" alt="sunrise"><br><sub><code>sunrise</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-rain.svg" width="56" height="56" alt="cloud-rain"><br><sub><code>cloud-rain</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-snow.svg" width="56" height="56" alt="cloud-snow"><br><sub><code>cloud-snow</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cloud-lightning.svg" width="56" height="56" alt="cloud-lightning"><br><sub><code>cloud-lightning</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/wind.svg" width="56" height="56" alt="wind"><br><sub><code>wind</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/snowflake.svg" width="56" height="56" alt="snowflake"><br><sub><code>snowflake</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/droplet.svg" width="56" height="56" alt="droplet"><br><sub><code>droplet</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/flame.svg" width="56" height="56" alt="flame"><br><sub><code>flame</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/leaf.svg" width="56" height="56" alt="leaf"><br><sub><code>leaf</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/tree.svg" width="56" height="56" alt="tree"><br><sub><code>tree</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/sprout.svg" width="56" height="56" alt="sprout"><br><sub><code>sprout</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/mountain.svg" width="56" height="56" alt="mountain"><br><sub><code>mountain</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/waves.svg" width="56" height="56" alt="waves"><br><sub><code>waves</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/flower.svg" width="56" height="56" alt="flower"><br><sub><code>flower</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bird.svg" width="56" height="56" alt="bird"><br><sub><code>bird</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fish.svg" width="56" height="56" alt="fish"><br><sub><code>fish</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/paw.svg" width="56" height="56" alt="paw"><br><sub><code>paw</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/umbrella.svg" width="56" height="56" alt="umbrella"><br><sub><code>umbrella</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/thermometer.svg" width="56" height="56" alt="thermometer"><br><sub><code>thermometer</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/rainbow.svg" width="56" height="56" alt="rainbow"><br><sub><code>rainbow</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cactus.svg" width="56" height="56" alt="cactus"><br><sub><code>cactus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/mushroom.svg" width="56" height="56" alt="mushroom"><br><sub><code>mushroom</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/earth.svg" width="56" height="56" alt="earth"><br><sub><code>earth</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/volcano.svg" width="56" height="56" alt="volcano"><br><sub><code>volcano</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/moon-star.svg" width="56" height="56" alt="moon-star"><br><sub><code>moon-star</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/tornado.svg" width="56" height="56" alt="tornado"><br><sub><code>tornado</code></sub></td>
<td></td>
<td></td>
</tr>
</table>

### Gaming (30)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/sword.svg" width="56" height="56" alt="sword"><br><sub><code>sword</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/swords.svg" width="56" height="56" alt="swords"><br><sub><code>swords</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/shield-sword.svg" width="56" height="56" alt="shield-sword"><br><sub><code>shield-sword</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/gamepad.svg" width="56" height="56" alt="gamepad"><br><sub><code>gamepad</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/joystick.svg" width="56" height="56" alt="joystick"><br><sub><code>joystick</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/dpad.svg" width="56" height="56" alt="dpad"><br><sub><code>dpad</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/dice.svg" width="56" height="56" alt="dice"><br><sub><code>dice</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/puzzle.svg" width="56" height="56" alt="puzzle"><br><sub><code>puzzle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/trophy.svg" width="56" height="56" alt="trophy"><br><sub><code>trophy</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/crown.svg" width="56" height="56" alt="crown"><br><sub><code>crown</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/medal.svg" width="56" height="56" alt="medal"><br><sub><code>medal</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bow.svg" width="56" height="56" alt="bow"><br><sub><code>bow</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/bomb.svg" width="56" height="56" alt="bomb"><br><sub><code>bomb</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/skull.svg" width="56" height="56" alt="skull"><br><sub><code>skull</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ghost.svg" width="56" height="56" alt="ghost"><br><sub><code>ghost</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/potion.svg" width="56" height="56" alt="potion"><br><sub><code>potion</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/target.svg" width="56" height="56" alt="target"><br><sub><code>target</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/crosshair.svg" width="56" height="56" alt="crosshair"><br><sub><code>crosshair</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/treasure-chest.svg" width="56" height="56" alt="treasure-chest"><br><sub><code>treasure-chest</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/castle.svg" width="56" height="56" alt="castle"><br><sub><code>castle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/helmet.svg" width="56" height="56" alt="helmet"><br><sub><code>helmet</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/armor.svg" width="56" height="56" alt="armor"><br><sub><code>armor</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/boots.svg" width="56" height="56" alt="boots"><br><sub><code>boots</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/spell-book.svg" width="56" height="56" alt="spell-book"><br><sub><code>spell-book</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/wizard-hat.svg" width="56" height="56" alt="wizard-hat"><br><sub><code>wizard-hat</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/chess-pawn.svg" width="56" height="56" alt="chess-pawn"><br><sub><code>chess-pawn</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cards.svg" width="56" height="56" alt="cards"><br><sub><code>cards</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/heart-health.svg" width="56" height="56" alt="heart-health"><br><sub><code>heart-health</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/level-up.svg" width="56" height="56" alt="level-up"><br><sub><code>level-up</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/coin-xp.svg" width="56" height="56" alt="coin-xp"><br><sub><code>coin-xp</code></sub></td>
</tr>
</table>

### Roblox Ui (37)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/player.svg" width="56" height="56" alt="player"><br><sub><code>player</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/leaderboard.svg" width="56" height="56" alt="leaderboard"><br><sub><code>leaderboard</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/inventory.svg" width="56" height="56" alt="inventory"><br><sub><code>inventory</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/backpack.svg" width="56" height="56" alt="backpack"><br><sub><code>backpack</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/health-bar.svg" width="56" height="56" alt="health-bar"><br><sub><code>health-bar</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/respawn.svg" width="56" height="56" alt="respawn"><br><sub><code>respawn</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/teleport.svg" width="56" height="56" alt="teleport"><br><sub><code>teleport</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/portal.svg" width="56" height="56" alt="portal"><br><sub><code>portal</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/checkpoint.svg" width="56" height="56" alt="checkpoint"><br><sub><code>checkpoint</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/map.svg" width="56" height="56" alt="map"><br><sub><code>map</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/radar.svg" width="56" height="56" alt="radar"><br><sub><code>radar</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/gems.svg" width="56" height="56" alt="gems"><br><sub><code>gems</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/xp.svg" width="56" height="56" alt="xp"><br><sub><code>xp</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/rank.svg" width="56" height="56" alt="rank"><br><sub><code>rank</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/quest.svg" width="56" height="56" alt="quest"><br><sub><code>quest</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/npc.svg" width="56" height="56" alt="npc"><br><sub><code>npc</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/emote.svg" width="56" height="56" alt="emote"><br><sub><code>emote</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/avatar.svg" width="56" height="56" alt="avatar"><br><sub><code>avatar</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/dash.svg" width="56" height="56" alt="dash"><br><sub><code>dash</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/double-jump.svg" width="56" height="56" alt="double-jump"><br><sub><code>double-jump</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fly.svg" width="56" height="56" alt="fly"><br><sub><code>fly</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/noclip.svg" width="56" height="56" alt="noclip"><br><sub><code>noclip</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/esp.svg" width="56" height="56" alt="esp"><br><sub><code>esp</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/halo.svg" width="56" height="56" alt="halo"><br><sub><code>halo</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/script-scroll.svg" width="56" height="56" alt="script-scroll"><br><sub><code>script-scroll</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/execute.svg" width="56" height="56" alt="execute"><br><sub><code>execute</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/inject.svg" width="56" height="56" alt="inject"><br><sub><code>inject</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/hub.svg" width="56" height="56" alt="hub"><br><sub><code>hub</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/auto-farm.svg" width="56" height="56" alt="auto-farm"><br><sub><code>auto-farm</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/server-hop.svg" width="56" height="56" alt="server-hop"><br><sub><code>server-hop</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/rejoin.svg" width="56" height="56" alt="rejoin"><br><sub><code>rejoin</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fps-boost.svg" width="56" height="56" alt="fps-boost"><br><sub><code>fps-boost</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/sleep.svg" width="56" height="56" alt="sleep"><br><sub><code>sleep</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/aura.svg" width="56" height="56" alt="aura"><br><sub><code>aura</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/camera-lock.svg" width="56" height="56" alt="camera-lock"><br><sub><code>camera-lock</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/speed-boots.svg" width="56" height="56" alt="speed-boots"><br><sub><code>speed-boots</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/currency-robux.svg" width="56" height="56" alt="currency-robux"><br><sub><code>currency-robux</code></sub></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>

### Developer Tools (28)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/code.svg" width="56" height="56" alt="code"><br><sub><code>code</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/braces.svg" width="56" height="56" alt="braces"><br><sub><code>braces</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/terminal.svg" width="56" height="56" alt="terminal"><br><sub><code>terminal</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/database.svg" width="56" height="56" alt="database"><br><sub><code>database</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/api.svg" width="56" height="56" alt="api"><br><sub><code>api</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/plugin.svg" width="56" height="56" alt="plugin"><br><sub><code>plugin</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/git-branch.svg" width="56" height="56" alt="git-branch"><br><sub><code>git-branch</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/git-commit.svg" width="56" height="56" alt="git-commit"><br><sub><code>git-commit</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/git-merge.svg" width="56" height="56" alt="git-merge"><br><sub><code>git-merge</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/git-pull-request.svg" width="56" height="56" alt="git-pull-request"><br><sub><code>git-pull-request</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/binary.svg" width="56" height="56" alt="binary"><br><sub><code>binary</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/variable.svg" width="56" height="56" alt="variable"><br><sub><code>variable</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/function.svg" width="56" height="56" alt="function"><br><sub><code>function</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/regex.svg" width="56" height="56" alt="regex"><br><sub><code>regex</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/webhook.svg" width="56" height="56" alt="webhook"><br><sub><code>webhook</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/package.svg" width="56" height="56" alt="package"><br><sub><code>package</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/blocks.svg" width="56" height="56" alt="blocks"><br><sub><code>blocks</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/workflow.svg" width="56" height="56" alt="workflow"><br><sub><code>workflow</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/network.svg" width="56" height="56" alt="network"><br><sub><code>network</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/command.svg" width="56" height="56" alt="command"><br><sub><code>command</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/flask.svg" width="56" height="56" alt="flask"><br><sub><code>flask</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/rocket.svg" width="56" height="56" alt="rocket"><br><sub><code>rocket</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/key-code.svg" width="56" height="56" alt="key-code"><br><sub><code>key-code</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bracket-square.svg" width="56" height="56" alt="bracket-square"><br><sub><code>bracket-square</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/parentheses.svg" width="56" height="56" alt="parentheses"><br><sub><code>parentheses</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/lua-moon.svg" width="56" height="56" alt="lua-moon"><br><sub><code>lua-moon</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/console.svg" width="56" height="56" alt="console"><br><sub><code>console</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/git-compare.svg" width="56" height="56" alt="git-compare"><br><sub><code>git-compare</code></sub></td>
<td></td>
<td></td>
</tr>
</table>

### Transportation (26)

<table>
<tr>
<td align="center" width="16%"><img src="icons/tiles/car.svg" width="56" height="56" alt="car"><br><sub><code>car</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bus.svg" width="56" height="56" alt="bus"><br><sub><code>bus</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/truck.svg" width="56" height="56" alt="truck"><br><sub><code>truck</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/bike.svg" width="56" height="56" alt="bike"><br><sub><code>bike</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/motorcycle.svg" width="56" height="56" alt="motorcycle"><br><sub><code>motorcycle</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/train.svg" width="56" height="56" alt="train"><br><sub><code>train</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/tram.svg" width="56" height="56" alt="tram"><br><sub><code>tram</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/plane.svg" width="56" height="56" alt="plane"><br><sub><code>plane</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/helicopter.svg" width="56" height="56" alt="helicopter"><br><sub><code>helicopter</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ship.svg" width="56" height="56" alt="ship"><br><sub><code>ship</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/cargo-ship.svg" width="56" height="56" alt="cargo-ship"><br><sub><code>cargo-ship</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/tanker.svg" width="56" height="56" alt="tanker"><br><sub><code>tanker</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/sailboat.svg" width="56" height="56" alt="sailboat"><br><sub><code>sailboat</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/anchor.svg" width="56" height="56" alt="anchor"><br><sub><code>anchor</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/fuel.svg" width="56" height="56" alt="fuel"><br><sub><code>fuel</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/traffic-cone.svg" width="56" height="56" alt="traffic-cone"><br><sub><code>traffic-cone</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/parking.svg" width="56" height="56" alt="parking"><br><sub><code>parking</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/road.svg" width="56" height="56" alt="road"><br><sub><code>road</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/map-route.svg" width="56" height="56" alt="map-route"><br><sub><code>map-route</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/submarine.svg" width="56" height="56" alt="submarine"><br><sub><code>submarine</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ufo.svg" width="56" height="56" alt="ufo"><br><sub><code>ufo</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/scooter.svg" width="56" height="56" alt="scooter"><br><sub><code>scooter</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/taxi.svg" width="56" height="56" alt="taxi"><br><sub><code>taxi</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/ambulance.svg" width="56" height="56" alt="ambulance"><br><sub><code>ambulance</code></sub></td>
</tr>
<tr>
<td align="center" width="16%"><img src="icons/tiles/container.svg" width="56" height="56" alt="container"><br><sub><code>container</code></sub></td>
<td align="center" width="16%"><img src="icons/tiles/forklift.svg" width="56" height="56" alt="forklift"><br><sub><code>forklift</code></sub></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>


## Validation Report

What was actually checked for this release, and how.

**Icon pack**
- 428 icons in 15 categories, each in 3 variants (outline, filled, duotone) plus a preview tile
- SVG structure check on every file: well-formed XML, `viewBox="0 0 24 24"` on every outline/filled/duotone file, only `path`, `circle`, `rect`, `g`, `mask` and `defs` elements, no scripts, links or external references
- Name check: unique kebab-case names, the same names in all variants and in `manifest.json`
- Geometry check: no two icons with identical geometry
- Visual check: every outline icon was rendered in Chromium and the contact sheets were looked at category by category. `sword`, `refresh-cw` and `tools` were redrawn from scratch and inspected at large and small sizes. Filled variants were rendered and inspected for every category; duotone variants were rendered and inspected as samples, not one by one.

**Library (`Mugi`)**
- Compiled and statically analyzed with the real Luau compiler: no syntax errors
- Source check: line 1 is the only comment in the file, no non-ASCII characters (no emoji), no pink colors (the only magenta is a keypoint of the hue spectrum in the color picker)
- Run in a simulated Roblox environment (a strict mock that rejects unknown properties and wrong value types, with a fake file system and HTTP): window creation, every component, tags with icons, tab icons, search icon, notifications, popup color picker (hex, RGB, presets, cancel, done), background via link and via `og:image` page, bubble customization, all 428 icons drawing without errors, config save/load/delete with the HWID-or-account rule (same account other device: visible; other account same device: visible; both changed: hidden), delete confirmation, auto save, notification cleanup and full cleanup on `Destroy`
- **Not tested in the real Roblox client or in a real executor.** Behavior that depends on executor functions (`request`, `getcustomasset`, `gethwid`, file functions) follows their documented behavior but could differ per executor.

**Thumbnail**
- The thumbnail at the top of this file uses the Dropbox link you provided (`raw=1`). Dropbox could not be reached from the build environment, so the image was **not** downloaded or checked there. If it does not show on GitHub, download the image once, save it as `assets/thumbnail.png`, and replace the `src` of the first `<img>` with `assets/thumbnail.png`.

## Troubleshooting

**`attempt to call a nil value` right after the `loadstring` line**
The library failed to load - usually a stale GitHub raw cache shortly after a push
