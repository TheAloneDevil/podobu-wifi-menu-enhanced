# Enhanced Weather Module for Polybar

![Weather Module](Screenshots/2.png)

This is an updated version of the polybar themes compared to the original at https://github.com/adi1090x/polybar-themes - featuring modern enhancements like More scripts, More day to day use Models and more.

![Weather Full Moon](Screenshots/3.png)

Special feature: Full moon detection - shows a unique icon during full moon nights!

---

## Features

- Fetches weather data from OpenWeatherMap API
- Custom weather icons for different conditions (sun, moon, clouds, rain, etc.)
- Temperature-based color coding (cold/blue, hot/orange)
- Moon phase detection (shows special icon during full moon)
- 30-minute update interval
- Configurable city and API key
- Caching to reduce API calls

---

## Installation (Step by Step for Rookies)

### Step 1: Choose Where to Put Your Scripts

Decide where you want to store your script. For this example, we'll use `~/polybar-scripts/`.

Replace `~/YourPath/` in all file paths with your chosen directory.

### Step 2: Create the Directory

```bash
mkdir -p ~/polybar-scripts
```

### Step 3: Copy the Files

```bash
cp weather.sh ~/polybar-scripts/
cp user_modules.ini ~/polybar-scripts/
```

### Step 4: Make Script Executable

```bash
chmod +x ~/polybar-scripts/weather.sh
```

### Step 5: Configure Your Location and API Key

Edit `weather.sh` and update:

**Getting CITY_ID:**
1. Go to https://openweathermap.org/cities
2. Search for your city
3. The city ID is the number at the end of the URL
   - Example: For London, URL is `https://openweathermap.org/city/2643743` → CITY_ID = `2643743`

**Getting API_KEY:**
1. Go to https://home.openweathermap.org/api_keys
2. If you don't have an account, sign up at https://openweathermap.org
3. After logging in, go to API Keys section
4. Click "Create New API Key" - give it a name (e.g., "Newbar")
5. Copy the new key and paste it in weather.sh

Update these lines in `weather.sh`:
```bash
CITY_ID="1234567"  # Your city ID
API_KEY="your_api_key_here"  # Your OpenWeatherMap API key
```

### Step 6: Update Paths in user_modules.ini

Open `user_modules.ini` and change:
```
exec = ~/YourPath/weather.sh
```
to your actual path, for example:
```
exec = ~/polybar-scripts/weather.sh
```

### Step 7: Add to Polybar

Add the weather module to your polybar config:
```
modules-right = ... weather ...
```

Or copy the content from `user_modules.ini` to your existing user_modules.ini.

### Step 8: Restart Polybar

```bash
polybar kill
polybar &
```

---

## Customization

### Changing Update Interval

Edit `user_modules.ini`:
```ini
interval = 1800  # 30 minutes in seconds
```

### Changing City

Edit `weather.sh` line 8:
```bash
CITY_ID="1255955"  # Your city ID
```

### Changing Temperature Units

Edit `weather.sh` line 10:
```bash
UNITS="metric"    # metric (°C) or imperial (°F)
```

### Key Directory References

| File | Line | Description | Default | Change To |
|------|------|-------------|---------|-----------|
| weather.sh | 8 | City ID | 1255955 | Your city ID |
| weather.sh | 9 | API Key | Your key | Your API key |
| weather.sh | 14 | Cache file | ~/.cache/weather.json | ~/YourPath/weather.json |
| user_modules.ini | 7 | Script path | ~/YourPath/weather.sh | Your path |

---

## Requirements

- Linux with NetworkManager
- Polybar
- curl (for API calls)
- jq (optional, for better JSON parsing)
- OpenWeatherMap API key (free)

---

## Troubleshooting

### Weather shows N/A
- Check your API key is correct
- Check your CITY_ID is correct
- Make sure you have internet connection

### Icons not showing
- Make sure Nerd Fonts are installed
- Check your terminal uses a Nerd Font

---

## Credits

This is based on various polybar weather modules. Modified and enhanced for better functionality.