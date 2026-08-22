<div align="center">

# 🌸 MugiHub

### Lightweight, draggable UI library for Roblox scripts.

<p>
  <strong>Draggable Window · Tab & Section Navigation · Live Search · Dynamic Tags · Stackable Notifications</strong>
</p>

</div>

---

MugiHub is a self-contained Luau UI library for Roblox script interfaces. One file, no external dependencies, no asset pack to install — `loadstring` it and start calling `CreateWindow`. It ships with a full component set (button, toggle, slider, input, dropdown, keybind, social/copy row, collapsible read-me block), a built-in search index that jumps straight to any element across tabs, and a notification system that stacks cleanly in the top-right corner.

The visual identity is fixed: **white → soft pink (`#FF99CC`)** gradients and accents, dark rounded panels, monospace-free Gotham typography. There is no theme switcher — this is intentional, it keeps the UI visually consistent across every script that uses it.

---

## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [Window](#window)
- [Tags](#tags)
- [Tabs & Sections](#tabs--sections)
- [Components](#components)
  - [AddButton](#addbutton)
  - [AddToggle](#addtoggle)
  - [AddSlider](#addslider)
  - [AddInput](#addinput)
  - [AddDropdown](#adddropdown)
  - [AddKeybind](#addkeybind)
  - [AddParagraph](#addparagraph)
  - [AddSeperator](#addseperator)
  - [AddLine](#addline)
  - [AddSocial](#addsocial)
  - [AddReadMe](#addreadme)
- [Notifications](#notifications)
- [Search](#search)
- [Icons](#icons)
- [Compatibility](#compatibility)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Credits](#credits)

---

## Installation

MugiHub is a single Luau module. Load it with `loadstring` + `HttpGet` and call it like any other library:

```lua
local MugiHub = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/4MugiHub/MugiHub/main/MugiHub.lua"
))()
```

> Replace the URL with wherever you're hosting `MugiHub.lua`. The script returns a single table (`MugiHub_Library`) with two entry points: `CreateWindow` and `SetNotification`.

---

## Quick Start

Minimal working example:

```lua
local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "Example script",
})

local Tab = Window:CreateTab({ "Main" })
local Section = Tab:AddSection("General", true) -- true = open by default

Section:AddButton({
    "Say Hello",
    "Prints a message to the console",
    "rbxassetid://7734010488",
    function()
        print("Hello from MugiHub!")
    end
})
```

A slightly more complete window:

```lua
local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "Violence District",
    ["Tab Width"] = 105,
    SizeUi = UDim2.fromOffset(480, 275),
    Keybind = Enum.KeyCode.RightControl,
    Icon = "rbxassetid://135368942844516",
    Tags = { "v2.0", "Beta" },
})

local Tab = Window:CreateTab({ "Killer", "rbxassetid://0" })
local Section = Tab:AddSection("Skills", true)

Section:AddToggle({
    "Auto Skill Check",
    "Automatically hits skill checks",
    false,
    function(value)
        print("Auto Skill Check:", value)
    end
})

Section:AddSlider({
    "Skill Check Delay",
    "Reaction delay in milliseconds",
    1, 0, 500, 50,
    function(value)
        print("Delay set to", value)
    end
})
```

Every `Add*` call accepts either **positional arguments** (`Config[1]`, `Config[2]`, ...) or **named fields** (`Config.Title`, `Config.Content`, ...) — both work interchangeably, shown throughout this document.

---

## Window

```lua
MugiHub:CreateWindow(Config) -> Funcs
```

| Field | Positional | Type | Default | Description |
|---|---|---|---|---|
| Title | `[1]` | `string` | `""` | Window title, shown top-left |
| Description | `[2]` | `string` | `""` | Subtitle, shown after a `\|` separator |
| Tab Width | `[3]` | `number` | `105` | Width of the left sidebar |
| SizeUi | `[4]` | `UDim2` | `UDim2.fromOffset(480, 275)` | Overall window size |
| Keybind | `[5]` | `Enum.KeyCode` | `RightControl` | Show/hide toggle key |
| Icon | `[6]` | `string` | `rbxassetid://135368942844516` | Icon shown next to the title |
| Tags | `[7]` / `Config.Tags` | `table<string>` | — | Initial tag pills (max 3, see [Tags](#tags)) |

`CreateWindow` returns a `Funcs` table with:

```lua
Funcs:SetTitle(NewTitle: string)
Funcs:SetDescription(NewDescription: string)
Funcs:CreateTab(Config) -> Sections
Funcs.Tags -- see below
```

**Window behavior:**
- Dragged from the top bar (`Top` frame).
- **Minimize** (`—` button) shrinks the window to a small floating icon that can itself be dragged around and clicked to restore.
- **Close** (`X` button) opens a confirmation popup *inside* the window itself (not a separate floating GUI) — title "Close Window", description "WANT TO CLOSE THIS SCRIPT?", with **Cancel** and **Close** buttons. Closing destroys the entire GUI and sets `MugiHub_Library.Unloaded = true`.
- The configured `Keybind` toggles window visibility at any time.
- An AFK-prevention loop (`VirtualUser`) is started automatically as soon as the library loads — this runs independently of any window.

---

## Tags

Small pill labels displayed in the top bar, next to the description. **Maximum 3 tags** — a 4th `Add()` call is silently ignored (returns a no-op table) to prevent layout overflow.

```lua
Window.Tags:Add(Text: string) -> TagItem
Window.Tags:AddDynamic(Label: string, ValueFn: () -> any, RefreshInterval: number?) -> TagItem
Window.Tags:AddExecutorTag(RefreshInterval: number?) -> TagItem
```

`TagItem` exposes:

```lua
TagItem:Set(NewText: string)
TagItem:Remove()
```

**Static tag:**

```lua
Window.Tags:Add("v2.0")
```

**Dynamic tag** (re-evaluates on an interval, prefixed with `●`):

```lua
Window.Tags:AddDynamic("Ping", function()
    return math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()) .. "ms"
end, 2)
```

**Executor tag** — a convenience wrapper around `AddDynamic` that calls `identifyexecutor()` if it exists in the environment, falling back to `"Unknown"`:

```lua
Window.Tags:AddExecutorTag(5)
```

---

## Tabs & Sections

```lua
Window:CreateTab(Config) -> Sections
```

| Field | Positional | Type | Default |
|---|---|---|---|
| Name | `[1]` / `Config.Name` | `string` | `""` |
| Icon | `[2]` / `Config.Icon` | `string` | resolved automatically — see [Icons](#icons) |

```lua
local Tab = Window:CreateTab({ "Survivor", "rbxassetid://0" })
```

The first tab created is automatically selected. Each tab is fully indexed by [Search](#search).

```lua
Tab:AddSection(Title: string, OpenByDefault: boolean?) -> Item
```

Sections are collapsible groups inside a tab. Clicking the section header expands/collapses it with a rotating chevron and animated height. `Item` is the object every component method below is called on.

```lua
local Section = Tab:AddSection("Combat", true)
```

---

## Components

All components live under a `Section` (the `Item` table returned by `AddSection`). Every component call registers itself with the search index automatically.

### AddButton

```lua
Section:AddButton({ Title, Content, Icon, Callback })
```

| Arg | Type | Default |
|---|---|---|
| Title | `string` | `""` |
| Content | `string` | `""` |
| Icon | `string` | `rbxassetid://7734010488` |
| Callback | `function()` | no-op |

```lua
Section:AddButton({
    "Reset Character",
    "Respawns your character",
    "rbxassetid://7734010488",
    function()
        Player.Character:BreakJoints()
    end
})
```

### AddToggle

```lua
Section:AddToggle({ Title, Content, Default, Callback }) -> Funcs_Toggle
```

`Callback(value: boolean)` fires immediately once with the default value, then again on every switch. Returned `Funcs_Toggle` exposes `:Set(value)` and `.Value`.

```lua
local AutoFarm = Section:AddToggle({
    "Auto Farm", "Automatically collects nearby items", false,
    function(value) print("Auto Farm:", value) end
})
```

### AddSlider

```lua
Section:AddSlider({ Title, Content, Increment, Min, Max, Default, Callback }) -> Funcs_Slider
```

Draggable track + editable number box, synced both ways. `Callback(value: number)` fires on release and on manual text entry.

```lua
Section:AddSlider({
    "Field of View", "Camera FOV", 1, 70, 120, 90,
    function(value) workspace.CurrentCamera.FieldOfView = value end
})
```

### AddInput

```lua
Section:AddInput({ Title, Content, Default, Callback }) -> Funcs_Input
```

`Callback(value: string)` fires on `FocusLost`.

```lua
Section:AddInput({
    "Webhook URL", "Paste your Discord webhook", "",
    function(value) print("Webhook set:", value) end
})
```

### AddDropdown

```lua
Section:AddDropdown({ Title, Content, Multi, Options, Default, Callback }) -> Funcs_Dropdown
```

| Arg | Type | Notes |
|---|---|---|
| Multi | `boolean` | allow multiple selections |
| Options | `table<string>` | also accepts `Config.List` as an alias |
| Default | `table<string>` or `string` | single strings are auto-wrapped into a table |

```lua
local Target = Section:AddDropdown({
    "Target Priority", "Who to prioritize", false,
    { "Closest", "Lowest HP", "Random" }, "Closest",
    function(value) print("Selected:", value[1]) end
})
```

`Funcs_Dropdown` methods:

```lua
Funcs_Dropdown:Set(Value: table<string>)
Funcs_Dropdown:AddOption(OptionName: string)
Funcs_Dropdown:Clear()
Funcs_Dropdown:Refresh(List: table<string>, Selecting: table<string>?)
```

Options open in a shared overlay panel with a built-in search box for filtering long lists.

### AddKeybind

```lua
Section:AddKeybind({ Title, Content, Default, Callback }) -> Funcs_Keybind
```

Click the keybind button, then press any key to rebind. `Callback(key: Enum.KeyCode)` fires every time the bound key is pressed while the window isn't consuming input.

```lua
Section:AddKeybind({
    "Toggle ESP", "", Enum.KeyCode.E,
    function() print("ESP key pressed") end
})
```

### AddParagraph

```lua
Section:AddParagraph({ Title, Content }) -> Funcs
```

Static text block, auto-wraps and resizes. `Funcs:Set({ Title, Content })` updates it later.

### AddSeperator

```lua
Section:AddSeperator({ Title })
```

A labeled divider bar between groups of components.

### AddLine

```lua
Section:AddLine()
```

A thin decorative spacer bar with no text.

### AddSocial

```lua
Section:AddSocial({ Icon, Title, Code }) -> Funcs
```

A row with an optional platform icon, a label, and a **Copy** button (uses `setclipboard` if available in the executor). The button label flips to "Copied" for 3 seconds after a click.

```lua
Section:AddSocial({
    "rbxassetid://0", "Join our Discord", "discord.gg/example"
})
```

`Funcs:SetCode(NewCode: string)` updates the copied value.

### AddReadMe

```lua
Section:AddReadMe({ Title, Content, Style, Open }) -> Funcs
```

| Style | Behavior |
|---|---|
| `"Accordion"` (default) | Collapsible block with a rotating chevron |
| `"Plain"` | Always expanded, no header button |
| `"Badge"` | Compact one-line pill: `Title \| Content` |

```lua
Section:AddReadMe({
    "About", "This script is provided as-is for educational purposes.", "Accordion", false
})
```

`Funcs` exposes `:Set(NewContent)`, `:SetTitle(NewTitle)`, and `:SetOpen(bool)` (Accordion style only).

---

## Notifications

```lua
MugiHub:SetNotification({ Text, Delay, Time }) -> { Close: function }
```

| Field | Type | Default |
|---|---|---|
| Text | `string` | `""` |
| Delay | `number` | `3` — seconds visible before auto-dismiss |
| Time | `number` | `0.25` — slide in/out animation duration |

```lua
MugiHub:SetNotification({ Text = "Auto Farm: enabled", Delay = 3 })
```

Notifications render in a dedicated top-right `ScreenGui`, independent of any window — they work even before `CreateWindow` is called. Each notification is a fixed-width (260px) dark card with a thin pink progress bar that shrinks over `Delay` seconds and auto-closes. Cards stack downward and don't reflow when new ones stack width-wise, since width is fixed. Call `:Close()` on the returned table to dismiss early.

---

## Search

Every component (`AddButton`, `AddToggle`, `AddSlider`, `AddInput`, `AddDropdown`, `AddKeybind`, `AddParagraph`, `AddSocial`, `AddReadMe`) auto-registers its title into a per-window search index. Typing into the sidebar search box:

1. Filters matches by substring (case-insensitive), capped at 8 results.
2. Shows a result list with the tab/section as a subtitle.
3. Clicking a result switches to the correct tab, expands the correct section if needed, scrolls it into view, and briefly highlights it with a pink glow ring.

No setup required — this is automatic for every component you add.

---

## Icons

Any `Icon` field across the library (window icon, tab icon, button icon) accepts a standard `rbxassetid://...` string. If you pass `""`, `nil`, or `"rbxassetid://0"`, it automatically resolves to MugiHub's default icon (`rbxassetid://135368942844516`) instead of rendering blank.

```lua
Tab.Icon = "rbxassetid://0" -- resolves to the default icon automatically
```

---

## Compatibility

| Environment | Support |
|---|---|
| Roblox Executor (`gethui`/`cloneref`) | ✅ Parents to `gethui()`, falling back to `cloneref(CoreGui)`, then raw `CoreGui` |
| Roblox Studio | ✅ Parents to `PlayerGui` (detected via `RunService:IsStudio()`) |
| Touch / Mobile | ✅ All drag, button, and slider interactions handle `Enum.UserInputType.Touch` |
| Mouse / Desktop | ✅ Standard `MouseButton1` / `MouseMovement` handling throughout |
| Clipboard (`AddSocial`) | ⚠️ Requires `setclipboard` in the executor — wrapped in `pcall`, fails silently if unavailable |
| Executor tag (`AddExecutorTag`) | ⚠️ Requires `identifyexecutor()` — falls back to `"Unknown"` if unavailable |

---

## Best Practices

- Prefer named config fields (`{ Title = "...", Callback = ... }`) over positional ones in larger scripts — it's more resistant to reordering mistakes as the library evolves.
- Keep toggle/slider callbacks lightweight; they can fire on every frame of a drag (sliders) or immediately on creation (toggles).
- Group related controls into their own `AddSection` rather than one long section — it keeps the sidebar scroll manageable.
- Don't exceed 3 tags — a 4th call is a silent no-op, so check your tag count if one isn't appearing.
- Use `SetNotification` for state changes and events, not for constant/spammy updates — each one runs its own slide + bar tween.
- Pass `rbxassetid://0` (or omit `Icon` entirely) instead of guessing an ID when you don't have one — it resolves safely to the default icon.

---

## Troubleshooting

**UI doesn't appear at all**
Confirm the `loadstring(game:HttpGet(...))()` call succeeded and check your executor's console for HTTP errors. Also confirm you actually called `:CreateWindow(...)` — loading the module alone only registers `SetNotification` and internal AFK handling.

**Tab icon is blank**
Passing an empty string or `"rbxassetid://0"` is handled automatically via the icon fallback. If it's still blank, the asset ID itself may be invalid/deleted on Roblox's CDN — try `Custom.DefaultIcon`'s ID (`135368942844516`) to confirm the rendering path works, then swap in your real asset.

**4th tag doesn't show up**
This is expected — `MAX_TAGS` is hard-capped at 3 to prevent sidebar layout overflow. `Tags:Add()` beyond that returns a no-op object.

**Dropdown selection looks out of sync**
`Funcs_Dropdown:Set()` reads current selection state from its own `.Value` table, not from UI transparency — if you're mutating selection state outside of `:Set()`/`:AddOption()`, call `:Set(FD.Value)` afterward to force a re-render.

**Clipboard button always shows "Copy" even after clicking**
`setclipboard` isn't available in your executor. The click is wrapped in `pcall` so it fails silently rather than erroring — check your executor's clipboard API support.

**Notifications don't fire before the window exists**
They don't need to — `SetNotification` creates its own `ScreenGui` on first call, independent of `CreateWindow`.

---

## Credits

**MugiHub** — created by **DinoIjoNPC** (`dinooo`).

