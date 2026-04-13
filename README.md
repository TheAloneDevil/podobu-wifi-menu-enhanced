# Enhanced WiFi Menu for Linux Desktop

This package provides enhanced WiFi menu and status modules for Linux desktop.

---

<p align="center">
  <img src="Screenshots/4.png" width="400"/>
  <img src="Screenshots/2.png" width="400"/>
  <img src="Screenshots/3.png" width="400"/>
</p>

## Files Included

1. **wifimenu-podobu** - Main WiFi menu script
2. **network-wifi.sh** - WiFi status display script
3. **user_modules.ini** - Module configuration
4. **README.md** - This file

---

## Features

- Network scanning with signal strength
- Saved network detection
- Try Again feature for changed passwords
- Auto Connection toggle
- Network Information menu
- Remove All Saved Networks option
- Works with rofi, wofi, dmenu

---

## Installation

### Step 1: Create Directory
```bash
mkdir -p ~/.config/polybar/forest/scripts
```

### Step 2: Copy Files
```bash
cp wifimenu-podobu ~/.config/your_path/scripts/
cp network-wifi.sh ~/.config/your_path/scripts/
cp user_modules.ini ~/.config/your_path/scripts/
```

### Step 3: Make Executable
```bash
chmod +x ~/.config/your_path/scripts/wifimenu-podobu
chmod +x ~/.config/your_path/scripts/network-wifi.sh
```

### Step 4: Create Wrapper (Optional)
Create `~/.config/your_path/scripts/wifimenu.sh`:
```bash
#!/bin/bash
while true; do
    ~/.config/your_path/scripts/wifimenu-podobu "$@"
    [ $? -ne 42 ] && break
done
```
Then make it executable:
```bash
chmod +x ~/.config/your_path/scripts/wifimenu.sh
```

### Step 5: Update Paths in user_modules.ini
Open `user_modules.ini` in a text editor and edit these specific lines:

| Line | Edit This | Change To |
|------|-----------|----------|
| 5 | `exec = ~/YourPath/network-wifi.sh` | `exec = ~/.config/your_path/scripts/network-wifi.sh` |
| 10 | `label = "%{A1:~/YourPath/wifimenu.sh &:}%output%%{A}"` | `label = "%{A1:~/.config/your_path/scripts/wifimenu.sh &:}%output%%{A}"` |
| 11 | `click-left = ~/YourPath/wifimenu.sh` | `click-left = ~/.config/your_path/scripts/wifimenu.sh` |

After editing, the file should look like:
```ini
;; _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_

[module/network-wifi]
type = custom/script
exec = ~/.config/your_path/scripts/network-wifi.sh
interval = 1
tail = true
format = <label>
format-foreground = ${color.foreground}
label = "%{A1:~/.config/your_path/scripts/wifimenu.sh &:}%output%%{A}"
click-left = ~/.config/your_path/scripts/wifimenu.sh

;; _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_
```

### Step 6: Enable Module in polybar config
Open your polybar config file (e.g., `~/.config/your_path/config`):

1. Find the `[module/...]` section (around line 5-10) and add:
```ini
include-file = ~/.config/your_path/scripts/user_modules.ini
```

2. Find your bar section (e.g., `[bar/top]`) and add `network-wifi` to `modules-left` or `modules-right`:
```ini
[bar/top]
modules-left = network-wifi
```
Or if you want it on the right:
```ini
modules-right = network-wifi
```

**Note:** If you already have other modules listed, add `network-wifi` to the existing list (e.g., `modules-left = battery network-wifi`).

---

## Requirements

- Linux desktop
- NetworkManager
- rofi or wofi or dmenu
- Nerd Fonts

---

## Font Reference

This module uses the following fonts (T-n = font-n+1):

| Tag | Font Number | Font Name | Size |
|-----|-------------|-----------|------|
| T29 | font-28 | Iosevka Nerd Font | 12;4 |

**Note:** Ensure these fonts are defined in your polybar config. Add to your `config.ini`:

```ini
font-28 = "Iosevka Nerd Font:size=12;4"
```

For icons, you may also need Material Icons:
```ini
font-11 = "Material Icons Sharp:size=14"
font-12 = "Material Icons Sharp:size=16"
font-13 = "Material Icons Sharp:size=18"
font-14 = "Material Icons Sharp:size=20"
```

---

## Contribution

This is a customized version of the original wifimenu created by Jesús Arenas (podobu). I, Anindra Mohan Trivedi, have modified it to add modern features and improvements.

I claim no rights to the original work — only to provide additional support and styling.

## Credits

Based on wifimenu by Jesús Arenas (podobu)
