<div align="center">

# MugiHub

**A clean, modern UI library for Roblox script hubs.**

Pink-and-white theme · Search-everything sidebar · Built-in notifications · Optional multi-config webhook · Zero dependencies

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
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

MugiHub is a single-file Luau UI library for building script hub interfaces on Roblox. It ships with a searchable sidebar, a draggable window, a minimize bubble, a stacked notification system, a full set of ready-made components, and an **optional** webhook layer for sending your own events to Discord or any other HTTP endpoint.

The library only provides the *mechanism* — sending, queueing, rate limiting. It ships with **no pre-made events, titles, or colors**. You define exactly what gets sent and how it looks in your own calling script. This keeps the library generic and keeps you in full control of what data leaves the player's client.

No external dependencies. No build step. Just `loadstring` one URL.

## Features

- **Draggable window** with a minimize bubble that remembers its position
- **Minimize (`─`) / Close (`✕`)** buttons with a close confirmation dialog
- **Global search** — every component you add is searchable by title, jumps to its tab/section, and briefly highlights it
- **Dynamic + executor tags** in the header, auto-refreshing on an interval
- **Stacked notifications** (top-right) with an auto-closing progress bar
- **Full component set**: buttons, toggles, sliders, text inputs, dropdowns, keybinds, paragraphs, separators, dividers, social links, copy groups, and ReadMe blocks
- **Optional webhook system** — create as many independent configs as you need, each with its own URL, queue, and rate limit
- **Not tied to Discord** — any endpoint that accepts a JSON POST works
- Ripple click effect on every interactive element

## Installation

Add a single line to the top of your script:

```lua
local MugiHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()
```

That's it — `MugiHub` is the only variable you need. Everything else is accessed through it:

- `MugiHub.Library` — the UI library
- `MugiHub.Webhook` — the optional webhook manager

> **Tip:** If you see `attempt to call a nil value` right after this line, it's almost always a briefly stale GitHub raw cache. Wait about a minute and run the script again.

## Quick Start

```lua
local MugiHub = loadstring(game:HttpGet("URL_HERE"))()

local Window = MugiHub.Library:CreateWindow({
    "My Script",
    "A short tagline",
    105,
    UDim2.fromOffset(480, 275),
    Enum.KeyCode.RightControl,
    "rbxassetid://18505728250",
})

local Tab = Window:AddTab({"Main", ""})
local Section = Tab:AddSection("General")

Section:AddToggle({
    "Example Toggle",
    false,
    function(value)
        print("Toggle is now:", value)
    end
})

MugiHub.Library:SetNotification({Content = "Loaded!", Delay = 3})
```

No other setup is required. The webhook system is entirely optional and only activates if you create a config and give it a URL.

## Window API

```lua
local Window = MugiHub.Library:CreateWindow({
    "Window Title",             -- [1] Title
    "Subtitle text",            -- [2] Description
    105,                        -- [3] Tab Width (pixels)
    UDim2.fromOffset(480, 275), -- [4] Size
    Enum.KeyCode.RightControl,  -- [5] Show/hide keybind
    "rbxassetid://...",         -- [6] Icon ("" to disable)
    {"TAG1", "TAG2"}            -- [7] Static tags (max 3)
})
```

| Method | Description |
|---|---|
| `Window:SetTitle(text)` | Updates the header title |
| `Window:SetDescription(text)` | Updates the header subtitle |
| `Window:AddTab({name, icon})` | Creates a new tab, returns a Tab object |

## Tags API

Accessible via `Window.Tags`.

```lua
local tag = Window.Tags:Add("LIVE")
tag:Set("UPDATED")
tag:Remove()

local dynamicTag = Window.Tags:AddDynamic("Players", function()
    return #game:GetService("Players"):GetPlayers()
end, 2) -- refreshes every 2 seconds

Window.Tags:AddExecutorTag(5) -- shows the current executor, refreshes every 5s
```

## Tab & Section API

```lua
local Tab = Window:AddTab({"Tab Name", "rbxassetid://..."})
local Section = Tab:AddSection("Section Title")
```

Every component below is added through a `Section` object.

## Components

### Button

```lua
Section:AddButton({
    "Do Something",
    "Runs a callback on click",
    function() end
})
```

### Toggle

```lua
local Toggle = Section:AddToggle({
    "Feature",
    false,
    function(value) end
})

Toggle.Set(true)
print(Toggle.Get())
```

### Slider

```lua
local Slider = Section:AddSlider({
    "Intensity",
    0, 100, 50,
    function(value) end
})
```

For decimal steps, use the `Increment` key:

```lua
Section:AddSlider({
    Name      = "Speed",
    Min       = 0,
    Max       = 1,
    Default   = 0.5,
    Increment = 0.1,
    Callback  = function(v) end,
})
```

### Input

```lua
local Input = Section:AddInput({
    "Message",
    "Placeholder...",
    "",
    function(value) end
})

Input.Set("hello")
print(Input.Get())
```

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
```

### Keybind

```lua
Section:AddKeybind({
    "Toggle Key",
    Enum.KeyCode.E,
    function(key) end
})
```

### Paragraph

```lua
local Paragraph = Section:AddParagraph({
    "Note",
    "Explanatory text that wraps across multiple lines."
})

Paragraph.Set("New content")
```

### Separator

```lua
Section:AddSeparator({"Advanced"})
Section:AddSeparator()
```

### Line

```lua
Section:AddLine()
```

### Social

```lua
Section:AddSocial({
    "Join Discord",
    "https://discord.gg/example",
    "rbxassetid://..."
})
```

### Copy Group

```lua
Section:AddCopyGroup({
    "Server IP",
    "play.example.com"
})
```

### ReadMe Component

```lua
Section:AddReadMe({
    "Getting Started",
    "Click to expand this section for setup instructions."
})
```

## Notifications

```lua
MugiHub.Library:SetNotification({
    Content = "Settings applied",
    Delay   = 3,
    Time    = 0.25
})

local notif = MugiHub.Library:SetNotification({Content = "Loading...", Delay = 10})
notif:Close()
```

## Search

Every component registered through a section is automatically searchable from the sidebar search box. Typing a query jumps to the matching tab, opens its section, scrolls it into view, and briefly highlights it — no extra setup needed.

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
    Color      = 0xFF99CC,
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
| `Color` | `0xFF99CC` | Fallback embed color when an event has none |

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
    color = 0xFF99CC,
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
    Color       = 0xFF99CC,
    Footer      = "My Script v1.0",
    Fields      = {
        { name = "Status", value = "Online", inline = true },
    },
})
```

Send several embeds in one request (Discord allows up to 10):

```lua
Log:SendEmbeds({
    { Title = "First",  Color = 0xFF99CC },
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

## Full Example

```lua
local MugiHub = loadstring(game:HttpGet("URL_HERE"))()

local Log = MugiHub.Webhook:NewConfig("Log", {
    URL = "https://discord.com/api/webhooks/ID/TOKEN",
})

Log:RegisterEvent("ButtonClicked", {title = "Button Clicked", color = 0xFF99CC})
Log:RegisterEvent("ToggleChanged", {title = "Toggle Changed", color = 0x99CCFF})

local Window = MugiHub.Library:CreateWindow({
    "My Script", "v1.0", 105,
    UDim2.fromOffset(480, 275),
    Enum.KeyCode.RightControl,
    "rbxassetid://18505728250",
})

MugiHub.Webhook:AttachToLibrary(MugiHub.Library, "Log")

local Tab = Window:AddTab({"Main", ""})
local Section = Tab:AddSection("General")

Section:AddButton({
    "Execute",
    "",
    function()
        Log:Send("ButtonClicked", {button = "Execute"})
    end
})

Section:AddToggle({
    "Feature",
    false,
    function(state)
        Log:Send("ToggleChanged", {toggle = "Feature", value = tostring(state)})
    end
})

MugiHub.Library:SetNotification({Content = "Script loaded!", Delay = 3})
```

## Troubleshooting

**`attempt to call a nil value` right after the `loadstring` line**
The library failed to load — this is almost always a stale GitHub raw CDN cache shortly after a push, or a restricted `loadstring`/HTTP function in your executor. Wait about 60 seconds and re-run. If it persists, try a different executor.

**Tab icon doesn't show up**
Confirm the asset ID is a real, public Image asset (not a Decal, Mesh, or a moderated/removed upload). The library falls back to a default icon automatically.

**Slider won't accept decimals**
Set the `Increment` key to a decimal value, e.g. `Increment = 0.1`.

**Webhook isn't sending**
- Confirm `URL` is set and correct
- Confirm your executor supports HTTP requests (`syn.request`, `http.request`, `request`, or `http_request`)
- Check `config:GetStats()` — a rising `failed` count means the URL or request itself is failing
- Try `config:Flush()` to force-send whatever is queued

**Want to test the webhook without Discord**
Use [webhook.site](https://webhook.site) — free, and shows incoming requests instantly.

## License

MIT — use it, fork it, ship it.
