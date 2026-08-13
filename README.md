# 🩷 MugiHub

**A modern, lightweight, and fully self-contained UI Library for Roblox Executors.**

Soft Pink & White themed · Search-driven navigation · Real-time tags · Copy-to-clipboard social links · Stacked notifications · Zero dependencies

---

## 📖 Table of Contents

1. [About MugiHub](#-about-mugihub)
2. [Credits](#-credits)
3. [Installation](#-installation)
4. [Quick Start](#-quick-start)
5. [Feature List](#-feature-list)
6. [API Reference](#-api-reference)
7. [Theming](#-theming)
8. [Search System](#-search-system)
9. [Exit Confirmation](#-exit-confirmation)
10. [Defensive API Behavior](#-defensive-api-behavior)
11. [Best Practices](#-best-practices)
12. [Troubleshooting](#-troubleshooting)
13. [License](#-license)

---

## 🌸 About MugiHub

**MugiHub** is a purpose-built graphical interface library for the Roblox Executor ecosystem. It was engineered from the ground up to give script developers a clean, elegant, and highly interactive control panel that feels native, responsive, and — most importantly — *pleasant to look at*.

Unlike many UI kits that overload developers with configuration or lock them into rigid themes, MugiHub keeps things intentionally simple: **one cohesive Soft Pink + White identity**, a fully searchable interface, and an API designed to be picked up in minutes.

MugiHub is not a fork — it is an original, from-scratch implementation, built and refined iteratively with a strong focus on real-world usability: things like notification spam-safety, accordion-based documentation blocks, live-updating tags, copy-to-clipboard support links, and an exit-confirmation flow are not afterthoughts, they are core design decisions.

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

```lua
local MugiHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()

local Window = MugiHub:CreateWindow({
    Title       = "MugiHub",
    Description = "My Script",
    Tags        = {"v1.0", "Free"} -- Icon not required: defaults to the official MugiHub icon
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

### 🪟 Window System
- Fully draggable window (drag from the top bar)
- Minimize → collapses into a small draggable floating icon (official MugiHub icon, no color tint), click it again to restore
- Close button opens a small, backdrop-free **exit confirmation popup**
- Structured header: **Icon → Title (pink) → Separator → Description (grey) → Tags**, distinct fonts/weights for clear hierarchy
- Larger, easier-to-hit Close and Minimize buttons
- Title & Description editable at runtime (`Window:SetTitle()`, `Window:SetDescription()`)
- Global **KeyBind** to toggle the whole UI on/off (default: `RightControl`)
- Content clips correctly at the rounded corners — nothing (dropdown overlays included) spills outside the window

### 🏷️ Tag System
- Static text tags (`Window.Tags:Add("Free")`)
- **Real-time / dynamic tags** computed live from a function (`Window.Tags:AddDynamic(...)`), marked with a small `●` live-indicator
- Built-in **executor auto-detection tag** (`Window.Tags:AddExecutorTag()`)
- Editable (`:Set()`) / removable (`:Remove()`) — dynamic tags auto re-measure so the background is never shorter than the text
- **Right-anchored**, sitting snugly next to Minimize instead of floating with dead space
- **Maximum of 4 tags** — a 5th is safely ignored (with a console warning)

### 👤 Identity
- Avatar pulled from the local player's real Roblox thumbnail
- Username auto-**censored** (first 3 letters + `***`)

### 🔍 Search System
- Every element (buttons, toggles, sliders, dropdowns, keybinds, paragraphs, README blocks, social links) is **automatically indexed**
- Hand-drawn vector search icon (not an external asset — always renders), never overlaps the typed text
- Floating, fully opaque result popup with divider lines — tab list is hidden underneath, zero visual bleed-through
- Clicking a result switches tab → opens section → scrolls into view → highlights with a fading ring
- Active-tab indicator bar computed from real rendered position — always lines up with the label, at any list depth

### 🗂️ Navigation
- Unlimited Tabs (each with its own icon) and unlimited collapsible Sections per tab

### 🧩 Section Elements
| Element | Purpose |
|---|---|
| `AddParagraph` | Static title + description text block |
| `AddSeperator` / `AddSeparator` | Labeled divider line (both spellings work) |
| `AddLine` | Plain decorative divider |
| `AddButton` | Clickable action button |
| `AddToggle` | On/off switch |
| `AddSlider` | Draggable numeric slider — smooth on touch/mobile |
| `AddInput` | Free-text input box |
| `AddDropdown` | Single/multi-select dropdown with built-in search |
| `AddKeybind` | User-rebindable keybind element |
| `AddReadMe` | Docs block — **Accordion** / **Plain** / **Badge** styles |
| `AddSocial` | Support/social link row with a **Copy** button |

### 📋 Copy-to-Clipboard Social Links
- `Section:AddSocial({Icon, Title, Code})` — platform icon + name + a Lucide-style **Copy** button
- Copies `Code` via `setclipboard()`, label flips to **"Copied"** with an icon flash, reverts to **"Copy"** after 3 seconds
- Rapid re-clicking handled gracefully — no flicker, no stacked timers

### 🔔 Notification System
- Non-blocking — call repeatedly with **zero risk of errors**
- Automatic **stacking** via native `UIListLayout` (scales to any amount of spam)
- Built-in **countdown bar** depleting over the notification's lifetime
- Slide in/out animation, each notification fully independent

### 🎨 Visual Identity
- Single accent: **Pink Muda (Soft Pink)** `RGB(255, 153, 204)` + White
- Solid pink for text/icons/fills; Pink→White gradient reserved for line/stroke elements (dividers, bars, borders)
- No preset theme system — one consistent identity

### 🖥️ Compatibility
- `gethui()` / `cloneref()` supported, Studio fallback to `PlayerGui`
- Full **Mouse** and **Touch** support, including smooth slider dragging on mobile

---

## 📚 API Reference

### `MugiHub:CreateWindow(Config)`

| Field | Type | Default | Description |
|---|---|---|---|
| `Title` | `string` | `""` | Window title (solid pink) |
| `Description` | `string` | `""` | Subtitle (dark grey, smaller/lighter font) |
| `["Tab Width"]` | `number` | `105` | Sidebar width in pixels |
| `SizeUi` | `UDim2` | `480x275` | Overall window size |
| `Keybind` | `Enum.KeyCode` | `RightControl` | Toggles the whole UI |
| `Icon` | `string` (rbxassetid) | `"rbxassetid://135368942844516"` | No color tint, avatar-thumbnail size. `""` hides it |
| `Tags` | `table<string>` | `{}` | Initial static tags (max 4 total) |

**Returns:** `Window` — `:CreateTab()`, `:SetTitle()`, `:SetDescription()`, `.Tags`.

```lua
local Window = MugiHub:CreateWindow({
    Title       = "MugiHub",
    Description = "Test Build",
    ["Tab Width"] = 105,
    SizeUi      = UDim2.fromOffset(480, 275),
    Keybind     = Enum.KeyCode.RightControl,
    Tags        = {"v1.0", "Free", "Test Mode"}
})
```

`Window:SetTitle(NewTitle)` / `Window:SetDescription(NewDescription)` — edit at runtime, auto-repositions everything after it.

### `Window.Tags`

Right-anchored next to Minimize. **Max 4 tags** — a 5th is ignored with a `warn()`.

```lua
local FreeTag = Window.Tags:Add("Free")
FreeTag:Set("Premium")
FreeTag:Remove()

-- Real-time tag — value computed live, not typed manually
Window.Tags:AddDynamic("Ping", function()
    return math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()) .. "ms"
end, 5) -- refresh every 5s

-- Shortcut: live executor detection
Window.Tags:AddExecutorTag(10)
```

### `Window:CreateTab(Config)`

`Config[1]`/`Name` = tab name, `Config[2]`/`Icon` = tab icon (optional).

```lua
local MainTab = Window:CreateTab({"Main", "rbxassetid://0"})
```

### `Tab:AddSection(Title, OpenSection)`

```lua
local Section = MainTab:AddSection("General", true)
```

### Section Elements

```lua
Section:AddParagraph({"Welcome", "Static info block."})

Section:AddSeparator({"Category Name"}) -- or AddSeperator, both work

Section:AddLine()

Section:AddButton({
    Title = "Click Me", Content = "Does a thing",
    Callback = function() print("clicked") end
})

local MyToggle = Section:AddToggle({
    Title = "Fast Walk", Default = false,
    Callback = function(Value) print(Value) end
})

Section:AddSlider({
    Title = "Walk Speed", Increment = 1, Min = 16, Max = 100, Default = 16,
    Callback = function(Value) print(Value) end
})

Section:AddInput({
    Title = "Display Name", Default = "MugiHub User",
    Callback = function(Value) print(Value) end
})

-- Dropdown: Options must be a table, Default must ALSO be a table (even single-select)
-- Callback ALWAYS receives a table — unwrap with value[1] for single-select.
local Dropdown = Section:AddDropdown({
    Title = "ESP Target", Multi = true,
    Options = {"Player", "Item", "NPC"}, Default = {"Player"},
    Callback = function(Value) print(table.concat(Value, ", ")) end
})
Dropdown:Refresh({"Player", "Item", "NPC", "Vehicle"}, {"Player"})
Dropdown:AddOption("Chest")
Dropdown:Clear()

Section:AddKeybind({
    Title = "Toggle Fast Walk", Default = Enum.KeyCode.F,
    Callback = function(Key) print(Key.Name) end
})

-- README: "Accordion" (collapsible, default) | "Plain" (static) | "Badge" (compact pill)
Section:AddReadMe({"About", "Full description...", "Accordion"})
Section:AddReadMe({"Note", "Always-visible text.", "Plain"})
Section:AddReadMe({"MugiHub", "by DinoIjoNPC", "Badge"})

-- Social link with Copy-to-clipboard button
Section:AddSocial({"rbxassetid://0", "Discord", "https://discord.gg/your-invite"})
```

Most elements return a `Handle` with `:Set(...)` to update it later; `AddReadMe` handles also expose `:SetTitle()`, and `AddSocial` handles expose `:SetCode(NewCode)`.

### `MugiHub:SetNotification(Config)`

| Field | Type | Default | Description |
|---|---|---|---|
| `Title` | `string` | `""` | Bold header |
| `Description` | `string` | `""` | Accent-colored subtitle next to Title |
| `Content` | `string` | `""` | Body text, auto-wraps |
| `Time` | `number` | `0.35` | Slide animation duration |
| `Delay` | `number` | `5` | Seconds before auto-close |

> 💡 Always use **named keys**. Positional args skip index 4 internally, so positional calls can silently shift `Time`/`Delay` into the wrong slots.

```lua
MugiHub:SetNotification({
    Title = "Success", Description = "Saved",
    Content = "Your settings have been saved.",
    Time = 0.35, Delay = 5
})
```

Non-blocking — call it repeatedly, back-to-back, with zero risk of errors; every notification stacks correctly.

---

## 🎨 Theming

- **Pink Muda (Soft Pink)** `RGB(255, 153, 204)` — solid, for text/icons/fills
- **White → Pink Muda gradient** — reserved for line/stroke elements (dividers, bars, tab indicators, borders)
- Title and Description intentionally use different fonts/colors (Title: bold pink; Description: regular grey, smaller) for clear hierarchy
- No preset theme system — one fixed, deliberate identity

---

## 🔍 Search System

Every element added via `Section:AddXXX(...)` is auto-indexed — no extra setup needed.

1. Type into the sidebar search box
2. A floating, fully opaque popup appears with divider lines between results — the tab list is **hidden** underneath, so there's never any bleed-through
3. Clicking a result: switches tab → opens section → scrolls into view → draws a fading pink highlight ring (~1.5s)

---

## ⚠️ Exit Confirmation

Clicking **X** no longer closes instantly — a small centered dialog appears, **without** a full-screen dimming backdrop:

> **"Are you sure you want to exit windows?"**
> `[Cancel]` (grey) &nbsp;&nbsp; `[Exit]` (red)

Cancel dismisses it; Exit closes the window for good.

---

## 🛡️ Defensive API Behavior

MugiHub tries to fail gracefully instead of crashing your whole script over a small mistake:

- **Dropdown `Options`** also accepts `List` as an alias key
- **Dropdown `Default`** — a bare string is auto-wrapped into a table (`"Instant"` → `{"Instant"}`) instead of erroring when `table.concat`/`table.find` run on it internally
- **`AddSeperator` / `AddSeparator`** — both spellings work
- **Tags** — a 5th tag past the limit is ignored with a `warn()`, not a crash

These are a safety net, not a substitute for using the correct API — always prefer `Options` + a table `Default`, as shown above.

---

## 💡 Best Practices

- Wrap `identifyexecutor`, `gethui`, `setclipboard` in `pcall` if extending MugiHub yourself — support varies by executor
- Prefer **named keys** over positional arguments for anything with 3+ fields
- Remember Dropdown callbacks always receive a table — unwrap with `value[1]` for single-select
- Use `AddReadMe("Badge")` for lightweight credits instead of adding more tags (remember: max 4)
- Group related settings under the same `Section` — accordions keep long tabs manageable

---

## 🛠️ Troubleshooting

**"attempt to index nil with 'X'" right after `CreateWindow`**
You may be loading a stale cached copy — GitHub raw content can be CDN-cached briefly after an update. Wait a minute and re-run.

**"invalid argument #1 to 'concat' (table expected, got string)"**
A `Dropdown`'s `Default` was passed as a plain string. MugiHub auto-corrects this defensively now, but fix it at the source: `Default = {"YourValue"}`, and read the callback value as `value[1]`.

**Tabs/sections don't appear at all**
An error likely occurred between `CreateWindow` and your `CreateTab` calls, halting the rest of the script. Check the console for the actual red error line — the text just above `Stack End` (which itself is just the trace footer, not the error).

**Notifications don't show / show in the wrong position**
Don't manually destroy MugiHub's ScreenGui elsewhere — the notification container is created once and reused for the session.

**Icons appear broken/red**
Verify the `rbxassetid://` is valid and public. Leave it as `""` to render blank (safe) instead.

**Window icon shows something other than MugiHub's branding**
Passing an explicit `Icon` in `CreateWindow` overrides the built-in MugiHub icon. Omit the field (or set `""`) to use the default branding icon.

---

## 📜 License

Provided as-is for personal and script-development use. Please keep credit to **DinoIjoNPC (dinooo)** intact when redistributing or building on top of this library.

---

<div align="center">

**MugiHub** — made with 🩷 by **DinoIjoNPC**

</div>
