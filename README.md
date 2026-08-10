# 🩷 MugiHub

**A modern, lightweight, and fully self-contained UI Library for Roblox Executors.**

Soft Pink & White themed · Search-driven navigation · Real-time tags · Stacked notifications · Zero dependencies

---

## 📖 Table of Contents

1. [About MugiHub](#-about-mugihub)
2. [Credits](#-credits)
3. [Installation](#-installation)
4. [Quick Start](#-quick-start)
5. [Feature List](#-feature-list)
6. [API Reference](#-api-reference)
   - [MugiHub:CreateWindow()](#mugihubcreatewindowconfig)
   - [Window.Tags](#windowtags)
   - [Window:CreateTab()](#windowcreatetabconfig)
   - [Tab:AddSection()](#tabaddsectiontitle-opensection)
   - [Section Elements](#section-elements)
   - [MugiHub:SetNotification()](#mugihubsetnotificationconfig)
7. [Theming](#-theming)
8. [Search System](#-search-system)
9. [Exit Confirmation](#-exit-confirmation)
10. [Best Practices](#-best-practices)
11. [Troubleshooting](#-troubleshooting)
12. [License](#-license)

---

## 🌸 About MugiHub

**MugiHub** is a purpose-built graphical interface library for the Roblox Executor ecosystem. It was engineered from the ground up to give script developers a clean, elegant, and highly interactive control panel that feels native, responsive, and — most importantly — *pleasant to look at*.

Unlike many UI kits that overload developers with configuration or lock them into rigid themes, MugiHub keeps things intentionally simple: **one cohesive Soft Pink + White identity**, a fully searchable interface, and an API designed to be picked up in minutes.

MugiHub is not a fork — it is an original, from-scratch implementation, built and refined iteratively with a strong focus on real-world usability: things like notification spam-safety, accordion-based documentation blocks, live-updating tags, and an exit-confirmation flow are not afterthoughts, they are core design decisions.

---

## 👑 Credits

| Role | Name |
|---|---|
| 🎨 UI Library Creator | **DinoIjoNPC** |
| 👤 Also known as | **dinooo** |
| 📦 Library Name | **MugiHub** |

MugiHub is built and maintained independently. If you use MugiHub in your own script, a small credit back to **DinoIjoNPC / dinooo** is always appreciated — it helps the project grow and keeps development active. ✨

---

## 📦 Installation

MugiHub is loaded entirely through a single `loadstring`. No additional files, no dependencies, no setup steps.

```lua
local MugiHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()
```

> ⚠️ **Note:** Make sure your executor has HTTP requests enabled (`game:HttpGet` must not be sandboxed/blocked). Almost all modern executors support this by default.

---

## 🚀 Quick Start

Below is the smallest possible working example — a window with one tab, one section, and one button.

```lua
local MugiHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()

local Window = MugiHub:CreateWindow({
    Title       = "MugiHub",
    Description = "My Script",
    Icon        = "rbxassetid://135368942844516",
    Tags        = {"v1.0", "Free"}
})

local MainTab     = Window:CreateTab({"Main", ""})
local MainSection = MainTab:AddSection("General", true)

MainSection:AddButton({
    Title    = "Hello World",
    Content  = "Click me to say hi",
    Callback = function()
        MugiHub:SetNotification({
            Title       = "Hi!",
            Description = "It works",
            Content     = "MugiHub is now running.",
            Time        = 0.35,
            Delay       = 4
        })
    end
})
```

That's it — no `:Init()`, no manual GUI parenting, no cleanup boilerplate. MugiHub handles all of it internally.

---

## ✅ Feature List

MugiHub ships with the following built-in systems, all working out of the box:

### 🪟 Window System
- Fully draggable window (drag from the top bar)
- Minimize → collapses into a small draggable floating icon, click it again to restore
- Close button with a built-in **exit confirmation popup** (prevents accidental closing)
- Structured header: **Icon → Title → Separator → Description → Tags**
- Title & Description are editable at runtime (`Window:SetTitle()`, `Window:SetDescription()`)
- Global **KeyBind** to toggle the whole UI on/off (default: `RightControl`, fully configurable)

### 🏷️ Tag System
- Static text tags (`Window.Tags:Add("Free")`)
- **Real-time / dynamic tags** — values computed live from a function, not hardcoded text (`Window.Tags:AddDynamic(...)`)
- Built-in **executor auto-detection tag** (`Window.Tags:AddExecutorTag()`) using `identifyexecutor()`
- Tags can be edited (`:Set()`) or removed (`:Remove()`) at any time
- No hard limit on tag count

### 👤 Identity
- Avatar automatically pulled from the local player's real Roblox thumbnail
- Username automatically **censored** (first 3 letters + `***`) for privacy in screenshots/streams

### 🔍 Search System
- Every single element you add (buttons, toggles, sliders, dropdowns, keybinds, paragraphs, README blocks) is **automatically indexed**
- Typing in the search bar shows a floating result popup — the tab list itself never changes or gets replaced
- Clicking a result: switches to the correct tab → opens the correct section → scrolls to the element → draws a temporary highlight ring around it

### 🗂️ Navigation
- Unlimited Tabs, each with its own icon
- Unlimited collapsible Sections (accordion-style) per tab

### 🧩 Section Elements
| Element | Purpose |
|---|---|
| `AddParagraph` | Static title + description text block |
| `AddSeperator` | Labeled divider line |
| `AddLine` | Plain decorative divider |
| `AddButton` | Clickable action button |
| `AddToggle` | On/off switch |
| `AddSlider` | Draggable numeric slider with manual text input |
| `AddInput` | Free-text input box |
| `AddDropdown` | Single or multi-select dropdown with built-in search |
| `AddKeybind` | User-rebindable keybind element |
| `AddReadMe` | Documentation block — 3 styles: **Accordion**, **Plain**, **Badge** |

### 🔔 Notification System
- Non-blocking — call it as many times as you want, back-to-back, with **zero risk of errors**
- Automatic vertical **stacking** powered by Roblox's native `UIListLayout` (no manual position math, scales to any amount of spam)
- Built-in **countdown bar** that visually depletes over the notification's lifetime
- Slide in / slide out animation
- Each notification is fully independent — closing one never affects another

### 🎨 Visual Identity
- Single accent color: **Pink Muda (Soft Pink) + White**
- Solid pink is used for text, icons, and fills
- Gradient (Pink → White) is reserved specifically for line/stroke-shaped elements (dividers, bars, borders) for visual depth
- No preset theme system — one consistent, deliberate identity

### 🖥️ Compatibility
- Works on Roblox Executors (`gethui()` / `cloneref()` supported, hidden from most detection methods)
- Automatic fallback to `Player.PlayerGui` when running inside Roblox Studio
- Full support for both **Mouse** and **Touch** (mobile) input

---

## 📚 API Reference

### `MugiHub:CreateWindow(Config)`

Creates and returns the main window. This is always the first function you call.

| Field | Type | Default | Description |
|---|---|---|---|
| `Title` | `string` | `""` | Window title text (rendered in pink) |
| `Description` | `string` | `""` | Subtitle text (rendered in dark grey) |
| `["Tab Width"]` | `number` | `105` | Width in pixels of the left sidebar |
| `SizeUi` | `UDim2` | `480x275` | Overall window size |
| `Keybind` | `Enum.KeyCode` | `RightControl` | Key that toggles the whole UI visible/hidden |
| `Icon` | `string` (rbxassetid) | `""` | Icon shown before the Title — rendered **with no color tint**, at avatar-thumbnail size |
| `Tags` | `table<string>` | `{}` | Initial list of static tags |

**Returns:** `Window` — a table containing `:CreateTab()`, `:SetTitle()`, `:SetDescription()`, and `.Tags`.

```lua
local Window = MugiHub:CreateWindow({
    Title       = "MugiHub",
    Description = "Test Build",
    ["Tab Width"] = 105,
    SizeUi      = UDim2.fromOffset(480, 275),
    Keybind     = Enum.KeyCode.RightControl,
    Icon        = "rbxassetid://135368942844516",
    Tags        = {"v1.0", "Free", "Test Mode"}
})
```

#### `Window:SetTitle(NewTitle: string)`
Changes the window title at runtime. Automatically repositions the separator, description, and tags.

#### `Window:SetDescription(NewDescription: string)`
Changes the window description at runtime. Automatically repositions the tags.

---

### `Window.Tags`

#### `Window.Tags:Add(Text: string) → TagHandle`
Adds a static text tag. Returns a handle with `:Set(NewText)` and `:Remove()`.

```lua
local FreeTag = Window.Tags:Add("Free")
FreeTag:Set("Premium") -- edit later
FreeTag:Remove()       -- or remove entirely
```

#### `Window.Tags:AddDynamic(Label: string, ValueFn: function, RefreshInterval: number?) → TagHandle`
Adds a **real-time** tag. Instead of a fixed string, the tag's value comes from `ValueFn()`, evaluated immediately and — if `RefreshInterval` is provided — re-evaluated automatically on that interval (in seconds).

```lua
-- Static example:  "Free"
-- Dynamic example:  "Executor: Delta"  (detected LIVE, not typed manually)

Window.Tags:AddDynamic("Ping", function()
    return math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()) .. "ms"
end, 5) -- refreshes every 5 seconds
```

#### `Window.Tags:AddExecutorTag(RefreshInterval: number?) → TagHandle`
A ready-made shortcut that detects the real executor name via `identifyexecutor()` and displays it as `Executor: <name>`. Falls back to `Executor: Unknown` if the executor doesn't support `identifyexecutor`.

```lua
Window.Tags:AddExecutorTag() -- one-time detection
Window.Tags:AddExecutorTag(10) -- re-checks every 10 seconds
```

---

### `Window:CreateTab(Config)`

| Index | Field | Description |
|---|---|---|
| `[1]` / `Name` | `string` | Tab name |
| `[2]` / `Icon` | `string` (rbxassetid) | Tab icon, optional |

```lua
local MainTab = Window:CreateTab({"Main", "rbxassetid://0"})
```

**Returns:** `Tab` — a table containing `:AddSection()`.

---

### `Tab:AddSection(Title, OpenSection)`

| Parameter | Type | Description |
|---|---|---|
| `Title` | `string` | Section header text |
| `OpenSection` | `boolean` | Whether the section starts expanded |

```lua
local Section = MainTab:AddSection("General", true)
```

**Returns:** `Section` — a table containing all element methods below.

---

### Section Elements

#### `Section:AddParagraph({Title, Content}) → Handle`
```lua
Section:AddParagraph({"Welcome", "This is a static info block."})
```
`Handle:Set({Title, Content})` — updates the text.

#### `Section:AddSeperator({Title}) → Handle`
```lua
Section:AddSeperator({"Category Name"})
```

#### `Section:AddLine()`
A plain decorative divider line, no parameters.

#### `Section:AddButton({Title, Content, Icon, Callback}) → Handle`
```lua
Section:AddButton({
    Title    = "Click Me",
    Content  = "Does a thing",
    Callback = function() print("clicked") end
})
```

#### `Section:AddToggle({Title, Content, Default, Callback}) → Handle`
```lua
local MyToggle = Section:AddToggle({
    Title    = "Fast Walk",
    Content  = "Enable extra speed",
    Default  = false,
    Callback = function(Value) print(Value) end
})
MyToggle:Set(true) -- toggle programmatically
```

#### `Section:AddSlider({Title, Content, Increment, Min, Max, Default, Callback}) → Handle`
```lua
Section:AddSlider({
    Title     = "Walk Speed",
    Content   = "Adjust movement speed",
    Increment = 1,
    Min       = 16,
    Max       = 100,
    Default   = 16,
    Callback  = function(Value) print(Value) end
})
```

#### `Section:AddInput({Title, Content, Default, Callback}) → Handle`
```lua
Section:AddInput({
    Title    = "Display Name",
    Default  = "MugiHub User",
    Callback = function(Value) print(Value) end
})
```

#### `Section:AddDropdown({Title, Content, Multi, Options, Default, Callback}) → Handle`
```lua
local Dropdown = Section:AddDropdown({
    Title    = "ESP Target",
    Multi    = true,
    Options  = {"Player", "Item", "NPC"},
    Default  = {"Player"},
    Callback = function(Value) print(table.concat(Value, ", ")) end
})
Dropdown:Refresh({"Player", "Item", "NPC", "Vehicle"}, {"Player"})
Dropdown:AddOption("Chest")
Dropdown:Clear()
```

#### `Section:AddKeybind({Title, Content, Default, Callback}) → Handle`
Creates a user-rebindable keybind. Clicking the bound-key button lets the user press any key to rebind it live.
```lua
Section:AddKeybind({
    Title    = "Toggle Fast Walk",
    Default  = Enum.KeyCode.F,
    Callback = function(Key) print("pressed:", Key.Name) end
})
```

#### `Section:AddReadMe({Title, Content, Style}) → Handle`
Three distinct display styles for documentation/description content:

| Style | Behavior |
|---|---|
| `"Accordion"` (default) | Collapsible block with a rotating chevron |
| `"Plain"` | Always-visible, static block — no collapsing |
| `"Badge"` | Small compact pill, ideal for credits/version info near buttons |

```lua
Section:AddReadMe({"About", "Full description text...", "Accordion"})
Section:AddReadMe({"Note", "Always-visible text.", "Plain"})
Section:AddReadMe({"MugiHub", "by DinoIjoNPC", "Badge"})
```
`Handle:Set(NewContent)` and `Handle:SetTitle(NewTitle)` are available on all three styles.

---

### `MugiHub:SetNotification(Config)`

| Field | Type | Default | Description |
|---|---|---|---|
| `Title` | `string` | `""` | Bold header text |
| `Description` | `string` | `""` | Accent-colored subtitle, shown next to Title |
| `Content` | `string` | `""` | Body text, wraps automatically |
| `Time` | `number` | `0.35` | Slide in/out animation duration (seconds) |
| `Delay` | `number` | `5` | How long the notification stays visible before auto-closing (seconds) |

> 💡 Always use **named keys** (`Title = ...`, `Delay = ...`) rather than positional array values — the 4th positional slot is intentionally reserved and skipped internally, so positional calls can silently shift `Time`/`Delay` into the wrong fields.

```lua
MugiHub:SetNotification({
    Title       = "Success",
    Description = "Saved",
    Content     = "Your settings have been saved.",
    Time        = 0.35,
    Delay       = 5
})
```

This function is **non-blocking** — call it repeatedly in a loop and every notification will stack correctly with zero risk of errors, no matter how fast or how many times you call it.

---

## 🎨 Theming

MugiHub uses one deliberate, fixed visual identity — there is no preset/theme switcher.

- **Pink Muda (Soft Pink)** `RGB(255, 153, 204)` — used solid for text, icons, and fills
- **White → Pink Muda gradient** — reserved exclusively for line/stroke-shaped elements: dividers, progress/countdown bars, tab indicators, card borders

This distinction keeps text and content easy to read while still giving structural elements (lines, bars, borders) a bit of visual depth.

---

## 🔍 Search System

Every element added through `Section:AddXXX(...)` is automatically registered into a global search index the moment it's created — you don't need to do anything extra.

1. Type into the sidebar's search box
2. A floating popup appears below it listing every match — **the tab list itself is never replaced or altered**
3. Click a result and MugiHub will automatically:
   - Switch to the correct Tab
   - Expand the correct Section (if collapsed)
   - Scroll the element into view
   - Draw a temporary pink highlight ring around it, which fades out after ~1.5 seconds

---

## ⚠️ Exit Confirmation

Clicking the **X (Close)** button no longer closes the window instantly. Instead, a small centered confirmation dialog appears:

> **"Are you sure you want to exit windows?"**
> `[Cancel]` (grey) &nbsp;&nbsp; `[Exit]` (red)

- **Cancel** dismisses the popup, the window stays open
- **Exit** closes the window for good

This prevents accidental closures from a stray click.

---

## 💡 Best Practices

- Always wrap `identifyexecutor`, `gethui`, and other executor-specific globals in `pcall` if you're extending MugiHub yourself — different executors implement different subsets of the API.
- Prefer **named keys** (`Title = ...`) over positional array arguments for anything with more than 2–3 fields — it's more readable and avoids index-order mistakes.
- Use `AddReadMe` with `"Badge"` style for lightweight credits/version info instead of cluttering the header with too many tags.
- Group related settings under the same `Section` — accordions keep long tabs manageable.

---

## 🛠️ Troubleshooting

**"attempt to index nil with 'X'" right after `CreateWindow`**
Make sure you're loading the *latest* raw file — GitHub raw content can be cached briefly by its CDN after an update. Wait a minute and re-run.

**Tabs/sections don't appear at all**
This almost always means an error occurred somewhere *between* `CreateWindow` and your `CreateTab` calls, which halts the rest of the script. Check your executor's console for the actual red error line (the text just above `Stack End` — `Stack End` itself is not the error, it's just the trace footer).

**Notifications don't show / show in the wrong position**
Make sure you're not manually destroying `MugiHub`'s ScreenGui elsewhere in your script — the notification container is created once and reused for the whole session.

**Icons appear as a broken/red image**
Double-check the `rbxassetid://` you provided is valid and public. An icon field left as `""` renders as blank (safe) rather than broken.

---

## 📜 License

MugiHub is provided as-is for personal and script-development use.
Please keep credit to **DinoIjoNPC (dinooo)** — the original creator of MugiHub — intact when redistributing or building on top of this library.

---

<div align="center">

**MugiHub** — made with 🩷 by **DinoIjoNPC**

</div>
