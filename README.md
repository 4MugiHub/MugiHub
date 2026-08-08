<div align="center">

# 🌸 MugiHub

**Modern Roblox UI Library**

*Clean UI · Pink & White Gradient · Adaptive DPI · Asset ID Support*

</div>

---

## Overview

**MugiHub** is a lightweight Roblox UI Library designed for clean, responsive interfaces across mobile, tablet, and PC.

It provides a simple API for building windows, tabs, sections, controls, notifications, keybinds, thumbnails, and README-style About pages.

---

## Installation

```lua
local Library = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"
))()
```

## Create a Window

```lua
local Window = Library:CreateWindow({
    Title = "My Script",
    Description = "My Game",
    Theme = "Pink",
    Icon = "rbxassetid://72876614672836",
})
```

| Property | Description |
|---|---|
| `Title` | Main window title |
| `Description` | Secondary window description |
| `Theme` | Accent theme |
| `Icon` | Window icon / Roblox Asset ID |
| `Thumbnail` | Optional thumbnail |

---

# Tabs

```lua
local Tab = Window:CreateTab({
    Name = "Main",
    Icon = "rbxassetid://10723407389",
})
```

Supported properties:

- `Name`
- `Icon`
- `Thumbnail`

Asset IDs may be supplied as either:

```lua
Icon = 123456789
```

or:

```lua
Icon = "rbxassetid://123456789"
```

---

# Sections / Accordion

```lua
local Section = Tab:AddSection("Player", true)
```

`true` opens the section by default. Use `false` to start collapsed.

---

# Toggle

```lua
Section:AddToggle({
    "God Mode",
    "Enable protection.",
    false,

    function(value)
        print("Enabled:", value)
    end
})
```

The callback receives a boolean.

---

# Button

```lua
Section:AddButton({
    "Execute",
    "Run the selected action.",
    "rbxassetid://10723407389",

    function()
        print("Clicked!")
    end
})
```

Use `""` when no icon is required.

---

# Slider

```lua
local Speed = Section:AddSlider({
    "WalkSpeed",
    "Adjust movement speed.",
    1,
    0,
    100,
    16,

    function(value)
        print("Speed:", value)
    end
})

Speed:Set(50)
```

Parameters:

| Position | Meaning |
|---|---|
| `1` | Title |
| `2` | Description |
| `3` | Increment |
| `4` | Minimum |
| `5` | Maximum |
| `6` | Default |
| `7` | Callback |

---

# Input

```lua
local Input = Section:AddInput({
    "Player Name",
    "Enter a username...",
    "",

    function(value)
        print("Input:", value)
    end
})

Input:Set("Dino")
```

---

# Dropdown

```lua
local Dropdown = Section:AddDropdown({
    "Target",
    "Select a target.",
    false,
    {
        "Player 1",
        "Player 2",
        "Player 3"
    },
    {},
    function(value)
        print(value[1])
    end
})
```

Use:

```lua
false
```

for single selection, or:

```lua
true
```

for multi-selection.

### Dropdown API

```lua
Dropdown:Set({"Player 1"})
Dropdown:Refresh({"New 1", "New 2"}, {})
Dropdown:AddOption("New 3")
Dropdown:Clear()
```

---

# KeyBind

MugiHub supports keyboard keybind controls.

```lua
local Bind = Section:AddKeybind({
    Title = "Toggle Menu",
    Content = "Press a key to activate.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(key)
        print("Pressed:", key.Name)
    end
})
```

The alternative capitalization is also supported:

```lua
Section:AddKeyBind({
    Title = "Example",
    Default = Enum.KeyCode.Insert,

    Callback = function(key)
        print(key.Name)
    end
})
```

Change the key:

```lua
Bind:Set(Enum.KeyCode.Insert)
```

---

# Paragraph

```lua
Section:AddParagraph({
    "Information",
    "This is an informational paragraph."
})
```

Useful for instructions, About pages, descriptions, and status information.

---

# Separator

```lua
Section:AddSeperator({
    "Advanced"
})
```

> The API name is `AddSeperator` as implemented by the library.

---

# Line

```lua
Section:AddLine()
```

Adds a visual divider.

---

# Notifications

```lua
Library:SetNotification({
    "MugiHub",
    "Loaded!",
    "Script successfully initialized.",
    nil,
    0.35,
    5,
})
```

| Position | Description |
|---|---|
| `1` | Title |
| `2` | Subtitle |
| `3` | Message |
| `4` | Optional value |
| `5` | Animation duration |
| `6` | Auto-close time |

---

# Thumbnail

Global thumbnail:

```lua
Window:SetThumbnail("https://example.com/image.png")
```

Tab thumbnail:

```lua
Window:SetTabThumbnail(
    0,
    "https://example.com/image.png"
)
```

---

# README / About Page

MugiHub supports README-style information directly inside the UI.

```lua
local Info = Window:CreateTab({
    Name = "About",
    Icon = ""
})

Info:AddReadme({
    SectionTitle = "About MugiHub?",
    Title = "What is MugiHub?",

    Content = [[
MugiHub is a modern Roblox UI Library.

It provides:
• Responsive UI
• Asset ID icons
• Tabs and sections
• Dropdowns
• Sliders
• Inputs
• KeyBinds
• Notifications
]]
})
```

Alias:

```lua
Info:AddREADME({
    SectionTitle = "About",
    Title = "MugiHub",
    Content = "Modern Roblox UI Library."
})
```

---

# Topbar Tags

```lua
Window:AddTag(
    "v1.0",
    Color3.fromRGB(80, 60, 100)
)
```

Multiple tags are supported:

```lua
Window:AddTag("Beta", Color3.fromRGB(60, 80, 120))
Window:AddTag("Free", Color3.fromRGB(80, 60, 100))
```

Executor information may also be displayed as a topbar tag when supported by the runtime environment.

---

# Minimize & Restore

MugiHub supports minimizing the window and restoring it through the small floating button.

```text
Window
  ↓
Minimize
  ↓
Floating restore button
  ↓
Window restored
```

The `X` button is separate from minimize and closes the interface.

---

# Search

MugiHub includes a search interface for navigating supported UI entries.

When the search field is cleared, the normal interface is restored.

---

# Complete Example

```lua
local Library = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"
))()

local Window = Library:CreateWindow({
    Title = "MyScript",
    Description = "My Game",
    Theme = "Pink",
    Icon = "rbxassetid://72876614672836",
})

Window:AddTag("v1.0", Color3.fromRGB(80, 60, 100))

Library:SetNotification({
    "MyScript",
    "Loaded!",
    "MugiHub initialized successfully.",
    nil,
    0.35,
    4,
})

local Main = Window:CreateTab({
    Name = "Main",
    Icon = "rbxassetid://10723407389",
})

local Section = Main:AddSection("Features", true)

Section:AddToggle({
    "Example Toggle",
    "Enable the example feature.",
    false,

    function(value)
        print("Toggle:", value)
    end
})

Section:AddButton({
    "Example Button",
    "Run an example action.",
    "rbxassetid://10723407389",

    function()
        print("Clicked!")
    end
})

Section:AddSlider({
    "Speed",
    "Example slider.",
    1,
    0,
    100,
    16,

    function(value)
        print("Value:", value)
    end
})

Section:AddDropdown({
    "Mode",
    "Select a mode.",
    false,
    {
        "Normal",
        "Fast",
        "Extreme"
    },
    {},
    function(value)
        print("Selected:", value[1])
    end
})

Section:AddInput({
    "Username",
    "Enter a username...",
    "",
    function(value)
        print("Username:", value)
    end
})

Section:AddKeybind({
    Title = "Example Key",
    Content = "Press a key.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(key)
        print("Key:", key.Name)
    end
})

local About = Window:CreateTab({
    Name = "About",
    Icon = ""
})

About:AddReadme({
    SectionTitle = "About MugiHub?",
    Title = "Modern Roblox UI Library",
    Content = [[
MugiHub is built for clean and responsive Roblox interfaces.

Thank you for using MugiHub.
]]
})
```

---

# Compatibility

MugiHub uses Roblox Luau and executor-side HTTP loading through `game:HttpGet`.

Compatibility can change as executors and their environments are updated.

| Executor | Status |
|---|---|
| Delta | ✅ |
| Arceus X | ✅ |
| Fluxus | ✅ |
| Hydrogen | ✅ |
| Solara | ✅ |
| Synapse X | ⚠️ Legacy / availability varies |
| Krnl | ⚠️ Availability varies |

> Compatibility is not guaranteed permanently. Executor updates may change supported APIs, rendering behavior, or HTTP behavior.

---

# Design

MugiHub focuses on:

- 🌸 Pink + White gradient styling
- 📱 Adaptive DPI scaling
- 🖥️ Mobile, tablet, and PC layouts
- 🖼️ Roblox Asset ID icons
- 🧩 Modular UI components
- 🔍 Search navigation
- ⌨️ KeyBind support
- 🔔 Notification system
- 📑 README / About pages
- 🏷️ Topbar tags
- 🖱️ Minimize and restore controls

---

# API Summary

| Component | API |
|---|---|
| Window | `Library:CreateWindow()` |
| Notification | `Library:SetNotification()` |
| Tab | `Window:CreateTab()` |
| Section | `Tab:AddSection()` |
| Toggle | `Section:AddToggle()` |
| Button | `Section:AddButton()` |
| Slider | `Section:AddSlider()` |
| Input | `Section:AddInput()` |
| Dropdown | `Section:AddDropdown()` |
| KeyBind | `Section:AddKeybind()` |
| KeyBind Alias | `Section:AddKeyBind()` |
| Paragraph | `Section:AddParagraph()` |
| Separator | `Section:AddSeperator()` |
| Line | `Section:AddLine()` |
| README | `Tab:AddReadme()` |
| README Alias | `Tab:AddREADME()` |
| Tag | `Window:AddTag()` |
| Thumbnail | `Window:SetThumbnail()` |

---

## License

**MugiHub · MIT License**

<div align="center">

🌸 **Built with MugiHub**

</div>
