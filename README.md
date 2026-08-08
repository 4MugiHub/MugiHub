<div align="center">

# 🌸 MugiHub
**Modern Roblox UI Library — Sakura Japan Theme**

*Pink & White Gradient · Adaptive DPI · All Devices*

</div>

---

## Instalasi

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()
```

---

## Membuat Window

```lua
local Window = Library:CreateWindow({
    Title       = "NamaScript",
    Description = "Nama Game",
    Theme       = "Pink",
    Icon        = "rbxassetid://72876614672836",
    Thumbnail   = "",
})
```

| Key | Fungsi | Default |
|---|---|---|
| `Title` | Judul window | `"MugiHub"` |
| `Description` | Badge di kanan judul | `""` (tidak muncul jika kosong) |
| `Theme` | Preset tema warna | `"Pink"` |
| `Icon` | Asset ID icon di topbar | default icon |
| `Thumbnail` | URL gambar thumbnail global | `nil` |

---

## Notifikasi Saat Execute

```lua
Library:SetNotification({
    "MugiHub",
    "Loaded!",
    "Script berhasil dijalankan.",
    nil, 0.35, 5,
})
```

---

## Tag Tambahan di Topbar

```lua
Window:AddTag("v1.0", Color3.fromRGB(80, 60, 100))
Window:AddTag("Beta",  Color3.fromRGB(60, 80, 120))
```

Tag muncul di kanan Description, bisa lebih dari satu.

---

## Membuat Tab

```lua
local Tab = Window:CreateTab({
    Name      = "Main",
    Icon      = "rbxassetid://10723407389",
    Thumbnail = "",
})
```

| Key | Fungsi |
|---|---|
| `Name` | Nama tab |
| `Icon` | Asset ID icon tab (kosong = tidak ada icon) |
| `Thumbnail` | URL thumbnail khusus tab ini |

---

## Membuat Section / Accordion

```lua
local Section = Tab:AddSection("Nama Section", true)
```

| Parameter | Fungsi |
|---|---|
| `"Nama Section"` | Judul |
| `true` | Buka saat load (`false` = tutup) |

---

## Toggle

```lua
Section:AddToggle({
    "Nama",
    "Deskripsi",
    false,
    function(value)
        print(value)
    end
})
```

---

## Button (dengan icon)

```lua
Section:AddButton({
    "Nama Button",
    "Deskripsi",
    "rbxassetid://10723407389",
    function()
        print("Klik!")
    end
})
```

Icon dikosongkan `""` jika tidak pakai.

---

## Card Button (tanpa icon, style card abu-abu)

```lua
Section:AddCardButton({
    "Nama Button",
    "Deskripsi",
    function()
        print("Klik!")
    end
})
```

Tampilan: rounded card abu-abu gelap, teks putih, tanpa image.

---

## Page Section (khusus Tab About/Main tanpa Accordion)

```lua
local Page = Tab:AddPageSection("https://link-thumbnail.com/img.jpg")

Page:AddButton({ "Tombol 1", function() end })
Page:AddButton({ "Tombol 2", function() end })
```

Setiap button punya corner sendiri. Tidak support Accordion.
Thumbnail opsional, kosongkan `""` jika tidak pakai.

---

## Slider

```lua
local MySlider = Section:AddSlider({
    "Nama",
    "Deskripsi",
    1,
    0,
    100,
    50,
    function(value)
        print(value)
    end
})

MySlider:Set(75)
```

| Index | Fungsi |
|---|---|
| 3 | Increment |
| 4 | Min |
| 5 | Max |
| 6 | Default |

---

## Input

```lua
local MyInput = Section:AddInput({
    "Nama",
    "Placeholder...",
    "",
    function(value)
        print(value)
    end
})

MyInput:Set("teks baru")
```

---

## Dropdown

```lua
local MyDrop = Section:AddDropdown({
    "Nama",
    "Deskripsi",
    false,
    {"Opsi A", "Opsi B", "Opsi C"},
    {},
    function(value)
        print(value[1])
    end
})
```

| Index 3 | `false` = single select · `true` = multi select |
|---|---|

```lua
MyDrop:Set({"Opsi A"})
MyDrop:Refresh({"Baru 1", "Baru 2"}, {})
MyDrop:AddOption("Opsi D")
MyDrop:Clear()
```

---

## Paragraph

```lua
Section:AddParagraph({
    "Judul",
    "Isi teks paragraph."
})
```

---

## Separator

```lua
Section:AddSeperator({ "Label" })
```

---

## Line

```lua
Section:AddLine()
```

---

## Notifikasi

```lua
Library:SetNotification({
    "Judul",
    "Subjudul",
    "Isi pesan.",
    nil,
    0.35,
    5,
})
```

| Index | Fungsi |
|---|---|
| 1 | Judul |
| 2 | Subjudul (warna accent) |
| 3 | Isi pesan |
| 5 | Durasi animasi |
| 6 | Detik sebelum auto-close |

Notif muncul di pojok kanan bawah. Jika ada notif baru, yang lama naik ke atas otomatis. Countdown bar pink di bagian bawah tiap notif.

---

## Theme Switcher

```lua
local Window = Library:CreateWindow({ Theme = "Purple" })

Window:SetTheme("Blue")
```

| Nama | Warna |
|---|---|
| `"Pink"` | Pink ← Default |
| `"Green"` | Hijau |
| `"Blue"` | Biru |
| `"Purple"` | Ungu |
| `"Red"` | Merah |
| `"Gold"` | Emas |
| `"Cyan"` | Cyan |
| `"Orange"` | Orange |

---

## Thumbnail

```lua
Window:SetThumbnail("https://link.com/img.jpg")
Window:SetTabThumbnail(0, "https://link.com/img.jpg")
```

---

## Minimize & Close

- **Minimize** → GUI hilang, muncul tombol kecil untuk restore
- **✕ Close** → Dialog konfirmasi muncul. **Tutup** = matikan semua script. **Batal** = kembali

---

## Executor Detection

MugiHub otomatis mendeteksi nama executor dan menampilkannya sebagai tag di topbar.

---

## Contoh Lengkap

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/4MugiHub/MugiHub/refs/heads/main/Mugi"))()

local Window = Library:CreateWindow({
    Title       = "MyScript",
    Description = "Game Name",
    Theme       = "Pink",
})

Library:SetNotification({
    "MyScript", "Loaded!", "Script aktif.", nil, 0.35, 4,
})

local Tab = Window:CreateTab({ Name = "Main", Icon = "rbxassetid://10723407389" })
local Sec = Tab:AddSection("Fitur", true)

Sec:AddToggle({
    "God Mode", "Tidak bisa mati", false,
    function(v) end
})

Sec:AddSlider({
    "Speed", "Kecepatan", 1, 16, 500, 16,
    function(v)
        local h = game.Players.LocalPlayer.Character
        if h and h:FindFirstChild("Humanoid") then
            h.Humanoid.WalkSpeed = v
        end
    end
})

local About = Window:CreateTab({ Name = "About", Icon = "" })
local Page  = About:AddPageSection("")
Page:AddButton({ "GitHub", function() end })
Page:AddButton({ "Discord", function() end })
```

---

## Changelog

### v1.0.0
- 🌸 Tema Sakura Jepang — Pink & White gradient
- ✅ Bunga sakura animasi di background window
- ✅ Description Badge — latar pink, teks putih
- ✅ Tag support — bisa lebih dari satu tag di topbar
- ✅ Executor auto-detect → tampil sebagai tag
- ✅ Notifikasi stack naik ke atas + countdown bar
- ✅ Button icon support semua asset ID
- ✅ Card Button — style tanpa icon, corner abu-abu
- ✅ Page Section — khusus tab tanpa accordion
- ✅ Dropdown dengan search + multi-select
- ✅ Adaptive DPI Scaling (HP/Tablet/PC)
- ✅ Scrolling support di semua tab
- ✅ Close dialog konfirmasi
- ✅ Theme Switcher 8 preset

---

## Requirements

| Executor | Support |
|---|---|
| Delta | ✅ |
| Arceus X | ✅ |
| Fluxus | ✅ |
| Hydrogen | ✅ |
| Solara | ✅ |
| Synapse X | ✅ |
| Krnl | ✅ |

---

<div align="center">
🌸 <b>MugiHub</b> · MIT License
</div>
