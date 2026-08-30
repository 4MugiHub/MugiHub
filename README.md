<div align="center">

# MugiHub

**A clean, modern UI library for Roblox script hubs.**

Pink-and-white theme · Search-everything sidebar · Built-in notifications · Zero dependencies

[![Lua](https://img.shields.io/badge/Lua-Luau-2C2D72?style=for-the-badge&logo=lua&logoColor=white)](https://luau-lang.org/)
[![Roblox](https://img.shields.io/badge/Platform-Roblox-000000?style=for-the-badge&logo=roblox&logoColor=white)](https://www.roblox.com/)
[![License](https://img.shields.io/badge/License-MIT-pink?style=for-the-badge)](#license)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Window API](#window-api)
- [Tags API](#tags-api)
- [Tab & Section API](#tab--section-api)
- [Components](#components)
  - [Button](#button)
  - [Toggle](#toggle)
  - [Slider](#slider)
  - [Input](#input)
  - [Dropdown](#dropdown)
  - [Keybind](#keybind)
  - [Paragraph](#paragraph)
  - [Separator](#separator)
  - [Line](#line)
  - [Social](#social)
  - [Copy Group](#copy-group)
  - [ReadMe](#readme-component)
- [Notifications](#notifications)
- [Search](#search)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

MugiHub is a single-file Luau UI library designed for building script hub interfaces on Roblox. It ships with a searchable sidebar, draggable window, minimize-to-bubble behavior, a stacked notification system, and a full set of ready-made components — all styled around a consistent pink-and-white accent theme.

No external dependencies. No build step. Just `loadstring` one URL and start building.

## Features

- **Draggable window** with a minimize bubble that remembers its position
- **Global search** — every component you add is searchable by title, jumps to its tab/section, and highlights it
- **Dynamic + executor tags** in the header, auto-refreshing on an interval
- **Stacked notifications** (top-right) with an auto-closing progress bar
- **Full component set**: buttons, toggles, sliders (with decimal support), text inputs, single/multi-select dropdowns, keybinds, paragraphs, separators, dividers, social/copy links, copy groups, and collapsible ReadMe blocks
- **Collapsible sections** with smooth expand/collapse animations
- **Ripple click effect** on every interactive element
- **Close confirmation dialog** to avoid accidental unloads

## Installation

Add this single line to the top of your script:

```lua
local Mugi = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()
```

That's it — `Mugi` now holds the library table and is ready to use.

> **Tip:** If you see `attempt to call a nil value` right after this line, it's almost always a briefly stale GitHub raw cache. Wait about a minute and run the script again.

## Quick Start

```lua
local Mugi = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()

local Window = Mugi:CreateWindow({
    Title       = "My Script",
    Description = "A short tagline",
    Tags        = {"v1.0", "FREE"}
})

local MainTab     = Window:CreateTab({"Main", "rbxassetid://135368942844516"})
local MainSection = MainTab:AddSection("General", true)

MainSection:AddToggle({
    Title    = "Example Toggle",
    Content  = "Does a thing when switched on",
    Default  = false,
    Callback = function(value)
        print("Toggle is now:", value)
    end
})

Mugi:SetNotification({
    Title       = "Loaded",
    Description = "Everything is ready",
    Delay       = 3
})
```

## Window API

```lua
local Window = Mugi:CreateWindow({
    Title       = "Window Title",      -- string
    Description = "Subtitle text",     -- string
    ["Tab Width"] = 105,                -- sidebar width in pixels
    SizeUi      = UDim2.fromOffset(480, 275),
    Keybind     = Enum.KeyCode.RightControl, -- show/hide shortcut
    Icon        = "rbxassetid://...",  -- header icon, "" to disable
    Tags        = {"TAG1", "TAG2"}      -- up to 3 static tags
})
```

| Method | Description |
|---|---|
| `Window:SetTitle(text)` | Updates the header title |
| `Window:SetDescription(text)` | Updates the header subtitle |
| `Window:CreateTab({name, icon})` | Creates a new tab, returns a Tab object |

## Tags API

Accessible via `Window.Tags`.

```lua
local tag = Window.Tags:Add("LIVE")
tag:Set("UPDATED")
tag:Remove()

local dynamicTag = Window.Tags:AddDynamic("Players", function()
    return #game:GetService("Players"):GetPlayers()
end, 2) -- refreshes every 2 seconds

Window.Tags:AddExecutorTag(5) -- shows the current executor name, refreshes every 5s
```

## Tab & Section API

```lua
local Tab = Window:CreateTab({"Tab Name", "rbxassetid://..."})
local Section = Tab:AddSection("Section Title", true) -- true = open by default
```

Every component below is added through a `Section` object.

## Components

### Button

```lua
Section:AddButton({
    Title    = "Do Something",
    Content  = "Runs a callback on click",
    Icon     = "rbxassetid://...", -- optional
    Callback = function() end
})
```

### Toggle

```lua
local Toggle = Section:AddToggle({
    Title    = "Feature",
    Content  = "Enables the feature",
    Default  = false,
    Callback = function(value) end
})

Toggle:Set(true) -- set programmatically
print(Toggle.Value)
```

### Slider

Supports decimal `Increment` values (e.g. `0.05`, `0.1`) as well as whole numbers, including manual entry in the numeric box.

```lua
local Slider = Section:AddSlider({
    Title     = "Intensity",
    Content   = "0 to 1, step 0.1",
    Increment = 0.1,
    Min       = 0,
    Max       = 1,
    Default   = 0.5,
    Callback  = function(value) end
})
```

### Input

```lua
local Input = Section:AddInput({
    Title    = "Message",
    Content  = "Free text field",
    Default  = "",
    Callback = function(value) end
})
```

### Dropdown

```lua
local Dropdown = Section:AddDropdown({
    Title    = "Mode",
    Content  = "Pick one",
    Multi    = false, -- true for multi-select
    Options  = {"Option A", "Option B", "Option C"},
    Default  = "Option A",
    Callback = function(values) print(values[1]) end
})

Dropdown:Set({"Option B"})
Dropdown:AddOption("Option D")
Dropdown:Refresh({"New", "List"}, {"New"})
Dropdown:Clear()
```

### Keybind

```lua
Section:AddKeybind({
    Title    = "Toggle Key",
    Content  = "Press to trigger",
    Default  = Enum.KeyCode.E,
    Callback = function(key) end
})
```

### Paragraph

```lua
local Paragraph = Section:AddParagraph({
    Title   = "Note",
    Content = "Explanatory text that can wrap across multiple lines."
})

Paragraph:Set({"New Title", "New content"})
```

### Separator

A plain text label used to visually group components within a section. Styled in the library's pink accent color.

```lua
Section:AddSeperator({Title = "Advanced"})
```

### Line

A thin horizontal divider with no text.

```lua
Section:AddLine()
```

### Social

A labeled row with a one-click "Copy" button — useful for Discord invites, usernames, etc.

```lua
local Social = Section:AddSocial({
    "rbxassetid://...",       -- platform icon
    "Join our Discord",       -- title
    "discord.gg/example"      -- text copied to clipboard
})

Social:SetCode("discord.gg/updated")
```

### Copy Group

A flexible grid of copy buttons. Pass a layout where each row is a list of `{Label, Code}` pairs — a row with one item spans the full width, a row with two or more items splits evenly.

```lua
Section:AddCopyGroup({
    Layout = {
        {{"Copy1", "value-one"}, {"Copy2", "value-two"}}, -- two buttons, one row
        {{"Copy3 (full width)", "value-three"}}            -- one button, full width
    }
})
```

### ReadMe Component

Three display styles: `"Accordion"` (collapsible), `"Plain"` (always expanded), `"Badge"` (compact single-line pill).

```lua
local ReadMe = Section:AddReadMe({
    "Getting Started",
    "Click to expand this section for setup instructions.",
    "Accordion",
    false -- start collapsed
})

ReadMe:Set({"New Title", "New content"})
ReadMe:SetTitle("Updated Title")
ReadMe:SetOpen(true)
```

## Notifications

Notifications stack in the top-right corner and close automatically after `Delay` seconds, with a shrinking progress bar.

```lua
Mugi:SetNotification({
    Title       = "Saved",       -- optional, combined with Description below
    Description = "Settings applied", -- optional
    Content     = "Extra detail",     -- optional
    Delay       = 3,             -- seconds before auto-close
    Time        = 0.25           -- slide animation duration
})
```

`Title`, `Description`, and `Content` are joined automatically if provided; you can also pass a single `Text` field directly if you prefer full control over the string.

```lua
local notif = Mugi:SetNotification({Text = "Custom message", Delay = 5})
notif:Close() -- dismiss early
```

## Search

Every component registered through a section is automatically searchable from the sidebar search box. Typing a query jumps to the matching tab, opens its section if collapsed, scrolls it into view, and briefly highlights it — no extra setup required on your end.

## Troubleshooting

**`attempt to call a nil value` right after the `loadstring` line**
The library failed to load — this is almost always a stale GitHub raw CDN cache shortly after a push, or a restricted `loadstring`/HTTP function in your executor. Wait about 60 seconds and re-run. If it persists across multiple attempts and multiple minutes, try a different executor to confirm.

**Tab icon doesn't show up**
Double-check the asset ID is a real, public Image asset (not a Decal, Mesh, or a moderated/removed upload). The library will automatically fall back to a default icon if the given ID fails to load.

**Slider won't accept decimals**
Make sure you're on the latest version of the library — earlier builds stripped decimal points from manual slider input.

## License

MIT — use it, fork it, ship it.
