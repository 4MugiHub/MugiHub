# MugiHub

<p align="center">
  <strong>A clean, modular, and developer-friendly Roblox UI Library.</strong>
</p>

<p align="center">
  Built for interfaces that feel organized, modern, responsive, and easy to maintain.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/MugiHub-Pink%20%7C%20White-ff69b4?style=for-the-badge" alt="MugiHub">
  <img src="https://img.shields.io/badge/Platform-Roblox-111111?style=for-the-badge" alt="Roblox">
  <img src="https://img.shields.io/badge/Language-Luau-00A2FF?style=for-the-badge" alt="Luau">
</p>

---

## ✦ About

**MugiHub** is a modular UI Library designed to make Roblox/Luau interfaces easier to build, organize, and maintain.

The library focuses on a structured Window system rather than forcing every project into the same layout. Developers can combine **Tabs, Accordions, Readme cards, Buttons, Toggles, Sliders, Inputs, KeyBinds, Dropdowns, and other controls** to create an interface that fits their project.

### Design principles

- **Clean** — information is separated into clear visual groups.
- **Readable** — text uses solid white for strong contrast and easier scanning.
- **Organized** — Tabs and Accordion containers keep large interfaces manageable.
- **Flexible** — informational content does not have to live in one special tab.
- **Developer-friendly** — controls expose straightforward callbacks and common methods.
- **Consistent** — the same visual language is used throughout the Window.

> MugiHub uses a **Pink → White** visual theme for UI surfaces while keeping interface text **solid white**. The original MugiHub icon is displayed without a pink tint.

---

# ✦ Installation

MugiHub can be loaded directly from the project's canonical raw GitHub endpoint.

### Load the Library

```lua
local MugiHub = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"
))()
```

### Recommended loader with error handling

```lua
local URL = "https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"

print("[MugiHub] Loading library...")

local Success, Library = pcall(function()
    return loadstring(game:HttpGet(URL))()
end)

if not Success then
    warn("[MugiHub] LOAD ERROR")
    warn("[MugiHub] " .. tostring(Library))
    return
end

if type(Library) ~= "table" or type(Library.CreateWindow) ~= "function" then
    warn("[MugiHub] API ERROR: CreateWindow is unavailable")
    return
end

print("[MugiHub] Library loaded successfully!")
print("[MugiHub] Test SUCCESS")
```

This loader separates **download/runtime errors** from **API validation errors**, making problems easier to diagnose.

---

# ✦ Quick Start

A minimal MugiHub Window can be created like this:

```lua
local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "My Project",
    Icon = "rbxassetid://121046122671218",

    Tags = {
        "Free",
        "Beta"
    },

    WelcomeText = "Welcome, username"
})
```

Create a Tab:

```lua
local Main = Window:CreateTab({
    "Main",
    "rbxassetid://ICON_ID"
})
```

Create an Accordion:

```lua
local General = Main:AddAccordion("General", false)
```

Then add controls:

```lua
General:AddButton({
    Title = "Test Button",
    Content = "Run a test action.",

    Callback = function()
        print("Button clicked")
    end
})
```

---

# ✦ Window System

The Window is the primary container for the library.

It provides a compact topbar and organized content area with support for:

| Component | Purpose |
|---|---|
| **Icon** | Displays the MugiHub/project icon |
| **Title** | Identifies the interface |
| **Description** | Adds contextual information beside the title |
| **Tags** | Displays compact status/category labels |
| **Search** | Quickly finds Tabs |
| **Tabs** | Separates major areas of the interface |
| **Active Indicator** | Clearly identifies the current Tab |
| **Avatar** | Displays the user's profile image |
| **Welcome Text** | Shows a personalized greeting |
| **Minimize** | Temporarily hides the main Window |
| **Floating Button** | Reopens the minimized interface |
| **Close Confirmation** | Prevents accidental closing |

### Original Icon

MugiHub's original icon asset is:

```text
121046122671218
```

The library does **not** recolor this asset.

---

# ✦ Tabs

Tabs are the highest-level navigation layer inside the Window.

```lua
local Main = Window:CreateTab({
    "Main",
    "rbxassetid://ICON_ID"
})
```

Use Tabs to separate major categories such as:

```text
Main
Settings
Visual
Utility
About
```

The sidebar Search can filter the available Tabs by name.

---

# ✦ Accordion System

MugiHub supports an accordion-style container for grouping related controls.

### Standard API

```lua
local Section = Main:AddSection("General", false)
```

### Explicit Accordion API

```lua
local Accordion = Main:AddAccordion("General", false)
```

Both APIs use the same underlying system.

`false` means the Accordion starts **closed**.

```lua
Main:AddAccordion("General", false)
```

`true` means it starts **open**.

```lua
Main:AddAccordion("General", true)
```

### Why use Accordions?

Accordions are useful when a Tab contains many controls. Instead of showing everything at once, related controls can be grouped into expandable sections.

Example:

```text
Main
│
├── General       [Closed]
├── Appearance    [Closed]
├── Advanced      [Closed]
└── Information   [Closed]
```

This keeps large interfaces easier to navigate.

---

# ✦ Readme / Information Cards

One of MugiHub's flexible components is the **Readme card**.

A Readme is an independent information block. It is **not a Button**, and it does not require a special `Info` tab.

### Basic usage

```lua
local Info = Main:AddAccordion("About", false)

Info:AddReadme({
    Title = "What is MugiHub?",
    Content = "MugiHub is a clean and modular Roblox UI Library."
})
```

### Alias

`AddInfo()` is also available:

```lua
Info:AddInfo({
    Title = "Information",
    Content = "Additional information for this section."
})
```

### Readme can be used anywhere

Readme cards are intentionally not restricted to one location.

For example:

```lua
local Settings = Main:AddAccordion("Settings", false)

Settings:AddReadme({
    Title = "Settings",
    Content = "Configure the available options in this section."
})
```

The same pattern can be used in any Accordion/Section.

### Accordion behavior

Because the Readme is inserted into the Accordion's content area, it follows the Accordion's state:

```text
Accordion CLOSED
└── Readme hidden

Accordion OPEN
└── Readme visible
```

This makes documentation, explanations, warnings, and section descriptions easy to place exactly where they are needed.

---

# ✦ Components

## Button

Use Buttons for actions.

```lua
Section:AddButton({
    Title = "Execute",
    Content = "Run the selected action.",

    Callback = function()
        print("Executed")
    end
})
```

---

## Toggle

Use Toggles for persistent on/off states.

```lua
local Toggle = Section:AddToggle({
    Title = "Enabled",
    Content = "Enable or disable the option.",
    Default = false,

    Callback = function(Value)
        print("Enabled:", Value)
    end
})
```

You can update it programmatically:

```lua
Toggle:Set(true)
```

---

## Slider

Sliders are useful for numeric settings.

```lua
local Slider = Section:AddSlider({
    Title = "Value",
    Content = "Choose a value from 0 to 100.",

    Min = 0,
    Max = 100,
    Increment = 1,
    Default = 50,

    Callback = function(Value)
        print("Value:", Value)
    end
})
```

The callback receives the current numeric value.

---

## Input

Use Input controls when users need to enter text.

```lua
local Input = Section:AddInput({
    Title = "Username",
    Content = "Enter a username.",
    Default = "",

    Callback = function(Value)
        print("Input:", Value)
    end
})
```

Set the value programmatically:

```lua
Input:Set("Dino")
```

---

## KeyBind

KeyBind allows users to select a keyboard key for an action.

```lua
local Keybind = Section:AddKeybind({
    Title = "Toggle UI",
    Content = "Press a key to activate the action.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(Key)
        print("Key:", Key.Name)
    end
})
```

The user can select the control and press another key to change the binding.

---

# ✦ Dropdowns

MugiHub supports both **Single Dropdown** and **Multi Dropdown**.

## Single Dropdown

Use this when only one option should be selected.

```lua
local Dropdown = Section:AddDropdown({
    Title = "Quality",
    Content = "Choose one quality level.",

    Multi = false,

    Options = {
        "Low",
        "Medium",
        "High"
    },

    Default = {
        "Medium"
    },

    Callback = function(Value)
        print("Selected:", Value)
    end
})
```

## Multi Dropdown

Use this when multiple options can be selected at the same time.

```lua
local Dropdown = Section:AddDropdown({
    Title = "Features",
    Content = "Select multiple features.",

    Multi = true,

    Options = {
        "ESP",
        "Notifications",
        "Auto Save",
        "Statistics"
    },

    Default = {
        "ESP",
        "Statistics"
    },

    Callback = function(Value)
        print("Selected options:", Value)
    end
})
```

### Refresh options

Dropdown options can be refreshed:

```lua
Dropdown:Refresh(
    {
        "New A",
        "New B",
        "New C"
    },
    {
        "New A"
    }
)
```

---

# ✦ Paragraph

Paragraphs are useful for simple descriptive content.

```lua
Section:AddParagraph({
    Title = "Information",
    Content = "This is a descriptive paragraph."
})
```

For larger documentation-style content, prefer **Readme**.

---

# ✦ Separator

Separators visually divide related controls.

```lua
Section:AddSeperator({
    Title = "Advanced"
})
```

> The spelling `AddSeperator` is intentionally preserved for API compatibility.

---

# ✦ Line

A simple line can be inserted with:

```lua
Section:AddLine()
```

---

# ✦ Complete Example

The following example demonstrates the major MugiHub systems together:

```lua
local MugiHub = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"
))()

local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "Complete UI Test",

    Icon = "rbxassetid://121046122671218",

    Tags = {
        "TEST",
        "BETA"
    },

    WelcomeText = "Welcome, username"
})

-- Main
local Main = Window:CreateTab({
    "Main",
    "rbxassetid://121046122671218"
})

local General = Main:AddAccordion("General", false)

General:AddReadme({
    Title = "What is MugiHub?",
    Content = "A clean and modular Roblox UI Library."
})

General:AddParagraph({
    Title = "Overview",
    Content = "This section demonstrates the core components."
})

General:AddButton({
    Title = "Test Button",
    Content = "Run the test callback.",

    Callback = function()
        print("[MugiHub] Button clicked")
    end
})

General:AddToggle({
    Title = "Test Toggle",
    Content = "Toggle a test state.",
    Default = false,

    Callback = function(Value)
        print("[MugiHub] Toggle:", Value)
    end
})

-- Controls
local Controls = Window:CreateTab({
    "Controls",
    "rbxassetid://121046122671218"
})

local ControlSection = Controls:AddAccordion("Controls", false)

ControlSection:AddSlider({
    Title = "Test Slider",
    Content = "Adjust a numeric value.",
    Min = 0,
    Max = 100,
    Increment = 1,
    Default = 50,

    Callback = function(Value)
        print("[MugiHub] Slider:", Value)
    end
})

ControlSection:AddInput({
    Title = "Test Input",
    Content = "Enter text.",
    Default = "",

    Callback = function(Value)
        print("[MugiHub] Input:", Value)
    end
})

-- Dropdowns
local DropdownTab = Window:CreateTab({
    "Dropdown",
    "rbxassetid://121046122671218"
})

local DropdownSection = DropdownTab:AddAccordion("Dropdown Tests", false)

DropdownSection:AddDropdown({
    Title = "Single",
    Content = "Choose one.",
    Multi = false,

    Options = {
        "A",
        "B",
        "C"
    },

    Default = {
        "A"
    },

    Callback = function(Value)
        print("[MugiHub] Single:", Value)
    end
})

DropdownSection:AddDropdown({
    Title = "Multiple",
    Content = "Choose multiple.",
    Multi = true,

    Options = {
        "A",
        "B",
        "C",
        "D"
    },

    Default = {
        "A",
        "C"
    },

    Callback = function(Value)
        print("[MugiHub] Multi:", Value)
    end
})

-- KeyBind
local KeybindTab = Window:CreateTab({
    "KeyBind",
    "rbxassetid://121046122671218"
})

local KeybindSection = KeybindTab:AddAccordion("KeyBind Test", false)

KeybindSection:AddKeybind({
    Title = "Test Key",
    Content = "Change the activation key.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(Key)
        print("[MugiHub] Key:", Key.Name)
    end
})

print("[MugiHub] Complete test loaded successfully!")
```

---

# ✦ Recommended UI Architecture

For larger projects, a structure like this keeps the interface maintainable:

```text
MugiHub Window
│
├── Topbar
│   ├── Icon
│   ├── Title
│   ├── Description
│   ├── Tags
│   ├── Minimize
│   └── Close
│
├── Sidebar
│   ├── Search
│   ├── Tabs
│   └── Avatar / Welcome
│
└── Content
    │
    └── Tab
        │
        ├── Accordion
        │   ├── Readme
        │   ├── Paragraph
        │   ├── Button
        │   └── Toggle
        │
        └── Accordion
            ├── Slider
            ├── Input
            ├── KeyBind
            └── Dropdown
```

### Why this structure works

**Tabs** represent broad categories.

**Accordions** represent groups within those categories.

**Readme cards** explain the purpose of a group.

**Controls** perform the actual interaction.

This hierarchy prevents a large UI from becoming one long, difficult-to-navigate list.

---

# ✦ API Overview

| API | Role |
|---|---|
| `CreateWindow()` | Creates the main Window |
| `CreateTab()` | Creates a navigation Tab |
| `AddSection()` | Creates an Accordion-style section |
| `AddAccordion()` | Explicit Accordion API |
| `AddReadme()` | Adds an information card |
| `AddInfo()` | Alias for Readme |
| `AddParagraph()` | Adds descriptive text |
| `AddButton()` | Adds an action Button |
| `AddToggle()` | Adds an on/off control |
| `AddSlider()` | Adds a numeric slider |
| `AddInput()` | Adds a text input |
| `AddKeybind()` | Adds a keyboard binding |
| `AddDropdown()` | Adds Single/Multi Dropdown |
| `AddSeperator()` | Adds a labeled separator |
| `AddLine()` | Adds a simple line |

---

# ✦ Compatibility Notes

MugiHub intentionally keeps several existing API names and behaviors for compatibility.

- `AddSection()` remains supported.
- `AddAccordion()` is available as the explicit Accordion API.
- `AddReadme()` works inside any returned Section/Accordion.
- `AddInfo()` is an alias for `AddReadme()`.
- Multi Dropdown is supported.
- KeyBind is supported.
- Slider, Input, Toggle, Button, Paragraph, Separator, and Line remain available.
- Search and Active Tab indication are part of the Window navigation.
- The Close button uses a confirmation step.
- The original icon is not recolored.
- Interface text remains solid white.
- The library includes a safe GUI-parent fallback for different runtime environments.

---

# ✦ Project Structure

A clean repository layout is recommended:

```text
MugiHub/
│
├── Mugi
├── README.md
└── Examples/
    └── CompleteTest.lua
```

The canonical library endpoint is:

```text
https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi
```

---

# ✦ Final Notes

MugiHub is designed around a simple idea:

> **Good UI should make a project easier to understand, not harder.**

Use **Tabs** for navigation, **Accordions** for organization, **Readme cards** for context, and controls for interaction.

Keep sections focused, use descriptive titles, and avoid placing too many unrelated controls into a single group.

That approach keeps the interface clean for users and the codebase easier for developers to maintain.

---

<p align="center">
  <strong>Built with MugiHub</strong>
</p>

<p align="center">
  Clean • Modular • Readable • Flexible
</p>
