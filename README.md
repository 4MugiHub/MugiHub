# MugiHub UI Library

Roblox/Luau UI Library dengan desain **Pink → White**, sementara seluruh text tetap **solid white**.

MugiHub menggunakan sistem Window dengan:
- original icon `121046122671218`
- floating open button
- topbar: icon, title, description, tags, minimize, close
- sidebar search
- icon tabs
- active-tab indicator
- avatar + `Welcome, username`
- accordion/section
- universal Readme/Info cards
- Button
- Toggle
- Slider
- Input
- KeyBind
- Single Dropdown
- Multi Dropdown
- Separator
- Line
- close confirmation

> Reference UI digunakan untuk **struktur Window/UI**, bukan untuk menyalin fitur gameplay.

---

## 1. Installation

Upload `MugiHub_Updated.lua` ke repository GitHub kamu.

Contoh:

```text
MugiHub/
├── MugiHub.lua
└── README.md
```

Buka file Lua di GitHub → **Raw**.

Kemudian load:

```lua
local MugiHub = loadstring(game:HttpGet(
    "YOUR_RAW_GITHUB_URL"
))()
```

Contoh format URL:

```text
https://raw.githubusercontent.com/USERNAME/REPOSITORY/main/MugiHub.lua
```

---

# 2. Create Window

```lua
local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "My Script",

    Tags = {
        "Free",
        "Beta"
    },

    Icon = "rbxassetid://121046122671218",

    WelcomeText = "Welcome, Dino"
})
```

### Window properties

| Property | Type | Keterangan |
|---|---|---|
| `Title` | string | Judul Window |
| `Description` | string | Deskripsi di topbar |
| `Icon` | string | Icon Window |
| `Logo` | string | Alias icon |
| `Tags` | table/string | Tag topbar |
| `Tag` | table/string | Alias Tags |
| `SearchIcon` | string | Icon Search |
| `WelcomeText` | string | Text profile |
| `Size` | UDim2 | Ukuran Window |

Default icon:

```lua
"rbxassetid://121046122671218"
```

Icon tersebut **tidak diberi tint pink** oleh library.

---

# 3. Tab

```lua
local Main = Window:CreateTab({
    "Main",
    "rbxassetid://ICON_ID"
})
```

Tab mendukung:
- icon
- active indicator
- sidebar search
- content page

Search otomatis mencari berdasarkan nama Tab.

---

# 4. Accordion / Section

MugiHub memiliki accordion-style container.

API lama:

```lua
local Section = Main:AddSection("General", true)
```

API baru yang lebih jelas:

```lua
local Accordion = Main:AddAccordion("General", true)
```

Keduanya menggunakan sistem yang sama.

`true`:

```lua
Main:AddAccordion("General", true)
```

= terbuka ketika dibuat.

`false`:

```lua
Main:AddAccordion("General", false)
```

= tertutup ketika dibuat.

---

# 5. Readme / Info Card

Readme adalah **card tersendiri**, bukan Button dan bukan bagian dari Button.

## Di dalam Accordion

```lua
local Info = Main:AddAccordion("About", true)

Info:AddReadme({
    Title = "What is MugiHub?",
    Content = "MugiHub is a personal UI Library project."
})
```

Readme otomatis:
- masuk ke dalam Accordion
- mengikuti ukuran Accordion
- ikut tersembunyi ketika Accordion ditutup
- ikut muncul ketika Accordion dibuka
- menyesuaikan tinggi berdasarkan panjang text

Alias:

```lua
Info:AddInfo({
    Title = "Information",
    Content = "This is an informational card."
})
```

## Bisa di Accordion mana pun

```lua
local Survivor = Main:AddAccordion("Survivor", true)

Survivor:AddReadme({
    Title = "Survivor Information",
    Content = "Information khusus untuk bagian Survivor."
})
```

Jadi Readme **tidak dibatasi pada Info/Main Menu**.

---

# 6. Paragraph

```lua
Section:AddParagraph({
    Title = "Title",
    Content = "Description..."
})
```

---

# 7. Button

```lua
Section:AddButton({
    Title = "Test",
    Content = "Run something.",
    Icon = "rbxassetid://7734010488",

    Callback = function()
        print("Clicked")
    end
})
```

---

# 8. Toggle

```lua
local Toggle = Section:AddToggle({
    Title = "Enabled",
    Content = "Enable the system.",
    Default = false,

    Callback = function(Value)
        print(Value)
    end
})
```

Set dari code:

```lua
Toggle:Set(true)
```

---

# 9. Slider

```lua
local Slider = Section:AddSlider({
    Title = "Walk Speed",
    Content = "Choose a value.",
    Increment = 1,
    Min = 1,
    Max = 100,
    Default = 16,

    Callback = function(Value)
        print(Value)
    end
})
```

---

# 10. Input

```lua
local Input = Section:AddInput({
    Title = "Username",
    Content = "Enter username.",
    Default = "",

    Callback = function(Value)
        print(Value)
    end
})
```

Set dari code:

```lua
Input:Set("Dino")
```

---

# 11. KeyBind

```lua
local Keybind = Section:AddKeybind({
    Title = "Toggle UI",
    Content = "Press a key.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(Key)
        print(Key.Name)
    end
})
```

User dapat menekan box KeyBind lalu menekan keyboard key baru.

---

# 12. Single Dropdown

```lua
local Dropdown = Section:AddDropdown({
    Title = "Select",
    Content = "Choose one.",

    Multi = false,

    Options = {
        "Option A",
        "Option B",
        "Option C"
    },

    Default = {
        "Option A"
    },

    Callback = function(Value)
        print(Value)
    end
})
```

---

# 13. Multi Dropdown

Multi Dropdown tetap didukung.

```lua
local Dropdown = Section:AddDropdown({
    Title = "Select Multiple",
    Content = "Choose multiple options.",

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
        print(Value)
    end
})
```

`Value` berupa table ketika `Multi = true`.

### Refresh

```lua
Dropdown:Refresh({
    "New A",
    "New B",
    "New C"
}, {
    "New A"
})
```

---

# 14. Separator

API yang tersedia:

```lua
Section:AddSeperator({
    Title = "Advanced"
})
```

> Nama `AddSeperator` dipertahankan agar kompatibel dengan API library saat ini.

---

# 15. Line

```lua
Section:AddLine()
```

---

# 16. Contoh Lengkap

```lua
local MugiHub = loadstring(game:HttpGet(
    "YOUR_RAW_GITHUB_URL"
))()

local Window = MugiHub:CreateWindow({
    Title = "MugiHub",
    Description = "Example Project",

    Tags = {
        "Free",
        "Beta"
    },

    Icon = "rbxassetid://121046122671218"
})

local Main = Window:CreateTab({
    "Main",
    "rbxassetid://ICON_ID"
})

local About = Main:AddAccordion("About", true)

About:AddReadme({
    Title = "What is MugiHub?",
    Content = "MugiHub is a clean and modular Roblox UI Library."
})

About:AddButton({
    Title = "Test Button",
    Content = "Click me.",

    Callback = function()
        print("Button clicked")
    end
})

About:AddToggle({
    Title = "Example Toggle",
    Content = "Enable or disable something.",
    Default = false,

    Callback = function(Value)
        print("Toggle:", Value)
    end
})

local Settings = Main:AddAccordion("Settings", false)

Settings:AddSlider({
    Title = "Value",
    Content = "Adjust the value.",
    Increment = 1,
    Min = 0,
    Max = 100,
    Default = 50,

    Callback = function(Value)
        print(Value)
    end
})

Settings:AddDropdown({
    Title = "Options",
    Content = "Select multiple options.",

    Multi = true,

    Options = {
        "A",
        "B",
        "C"
    },

    Default = {
        "A"
    },

    Callback = function(Value)
        print(Value)
    end
})

Settings:AddKeybind({
    Title = "Keybind",
    Content = "Change activation key.",
    Default = Enum.KeyCode.RightShift,

    Callback = function(Key)
        print("Pressed:", Key.Name)
    end
})
```

---

# 17. Recommended Structure

```text
MugiHub Window
│
├── Topbar
│   ├── Original Icon
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
    └── Tab
        └── Accordion
            ├── Readme
            ├── Paragraph
            ├── Button
            ├── Toggle
            ├── Slider
            ├── Input
            ├── KeyBind
            ├── Dropdown
            ├── Separator
            └── Line
```

---

# Compatibility

- `AddSection()` tetap tersedia.
- `AddAccordion()` adalah alias resmi untuk sistem Accordion.
- `Accordion:AddReadme()` didukung.
- `Accordion:AddInfo()` didukung sebagai alias.
- Readme dapat digunakan di Accordion mana pun.
- Multi Dropdown tetap tersedia.
- KeyBind tetap tersedia.
- Search tetap tersedia.
- Active Tab indicator tetap tersedia.
- Close confirmation tetap tersedia.
- Text tetap solid white.
- Original icon tidak diberi tint.
- Fitur gameplay dari UI referensi tidak disalin.

---

## License

Tambahkan license pilihanmu sebelum repository dipublikasikan.
