# Terminal Customization

I like my terminal to be like this :

```shell
uname@hostname:~
$
```

rather than this :

```shell
uname@hostname:~$
```

and also you can backup your data with this command :

```shell
dconf dump /org/gnome/terminal/ > ~/gnome_terminal_settings_backup.txt
```

Reset (wipe out) the settings before loading a new one (probably not really required):

```shell
dconf reset -f /org/gnome/terminal/
```

Load the saved settings:

```shell
dconf load /org/gnome/terminal/ < gnome_terminal_settings_backup.txt
```

# your entire dconf database

it is stored in the single file `~/.config/dconf/user` .

# My Setup

```plain
[legacy/profiles:]
default='b1dcc9dd-5262-4d8d-a863-c897e6d979b9'
list=['b1dcc9dd-5262-4d8d-a863-c897e6d979b9', 'adad0998-8247-48d8-a62b-6b5eb8f27dc9']

[legacy/profiles:/:adad0998-8247-48d8-a62b-6b5eb8f27dc9]
palette=['rgb(23,20,33)', 'rgb(192,28,40)', 'rgb(38,162,105)', 'rgb(162,115,76)', 'rgb(18,72,139)', 'rgb(163,71,186)', 'rgb(42,161,179)', 'rgb(208,207,204)', 'rgb(94,92,100)', 'rgb(246,97,81)', 'rgb(51,209,122)', 'rgb(233,173,12)', 'rgb(42,123,222)', 'rgb(192,97,203)', 'rgb(51,199,222)', 'rgb(255,255,255)']
use-theme-colors=true
visible-name='normal'

[legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9]
audible-bell=true
background-color='rgb(0,1,26)'
background-transparency-percent=51
font='Monospace 14'
foreground-color='rgb(0,172,161)'
highlight-colors-set=false
palette=['rgb(23,20,33)', 'rgb(192,28,40)', 'rgb(38,162,105)', 'rgb(162,115,76)', 'rgb(0,85,190)', 'rgb(163,71,186)', 'rgb(42,161,179)', 'rgb(208,207,204)', 'rgb(94,92,100)', 'rgb(246,97,81)', 'rgb(51,209,122)', 'rgb(233,173,12)', 'rgb(42,123,222)', 'rgb(192,97,203)', 'rgb(51,199,222)', 'rgb(255,255,255)']
use-system-font=false
use-theme-colors=false
use-theme-transparency=true
use-transparent-background=false
visible-name='mahdic200'
```

here is a shell script to import my color palette for yourself automatically :

```shell
#!/bin/bash
# Function to convert rgb(r, g, b) to hex format
rgb_to_hex() {
    # Extract numbers from rgb(r, g, b) format
    rgb=$1
    numbers=$(echo $rgb | grep -o '[0-9]\+')
    r=$(echo "$numbers" | sed -n '1p')
    g=$(echo "$numbers" | sed -n '2p')
    b=$(echo "$numbers" | sed -n '3p')
    
    # Convert to hex
    printf "#%02X%02X%02X" "$r" "$g" "$b"
}

# Function to get the profile UUID
get_profile_uuid() {
    # First try the Mint/Cinnamon specific path
    local uuid=$(gsettings get org.gnome.Terminal.ProfilesList default | tr -d "'")
    
    if [ -z "$uuid" ]; then
        # If that fails, try getting list of profiles
        local profile_list=$(gsettings get org.gnome.Terminal.ProfilesList list)
        # Get the first profile from the list if it exists
        uuid=$(echo "$profile_list" | grep -o "'[^']*'" | head -1 | tr -d "'")
    fi
    
    if [ -z "$uuid" ]; then
        # If still no UUID found, check alternative location
        uuid=$(dconf list /org/gnome/terminal/legacy/profiles:/ | grep '^:' | head -1 | tr -d '/:')
    fi

    echo "$uuid"
}

# Function to update color setting
update_color_setting() {
    local profile_uuid=$1
    local setting_name=$2
    local color_value=$3
    
    # Try gsettings first
    gsettings set "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile_uuid/" "$setting_name" "$color_value"
    
    # If gsettings fails, try dconf
    if [ $? -ne 0 ]; then
        dconf write "/org/gnome/terminal/legacy/profiles:/:$profile_uuid/$setting_name" "'$color_value'"
    fi
}

# Get the profile UUID
profile_uuid=$(get_profile_uuid)
if [ -z "$profile_uuid" ]; then
    echo "Error: Could not find terminal profile UUID"
    exit 1
fi

echo "Found profile UUID: $profile_uuid"

colors=("rgb(0,172,161)" "rgb(0,1,26)" "rgb(23,20,33)" "rgb(192,28,40)" "rgb(38,162,105)" "rgb(162,115,76)" "rgb(0,85,190)" "rgb(163,71,186)" "rgb(42,161,179)" "rgb(208,207,204)" "rgb(94,92,100)" "rgb(246,97,81)" "rgb(51,209,122)" "rgb(233,173,12)" "rgb(42,123,222)" "rgb(192,97,203)" "rgb(51,199,222)" "rgb(255,255,255)")

# Check if we have exactly 18 colors
if [ ${#colors[@]} -ne 18 ]; then
    echo "Error: Expected 18 colors, but found ${#colors[@]}"
    echo "Format should be: foreground, background, followed by 16 palette colors"
    exit 1
fi

# Convert and set foreground color
foreground=$(rgb_to_hex "${colors[0]}")
echo "Setting foreground color to $foreground"
update_color_setting "$profile_uuid" "foreground-color" "$foreground"

# Convert and set background color
background=$(rgb_to_hex "${colors[1]}")
echo "Setting background color to $background"
update_color_setting "$profile_uuid" "background-color" "$background"

# Process palette colors (remaining 16 colors)
palette_colors=()
for i in {2..17}; do
    hex=$(rgb_to_hex "${colors[$i]}")
    palette_colors+=("'$hex'")
done

# Set the palette
color_array="[$(IFS=,; echo "${palette_colors[*]}")]"
echo "Setting color palette"
update_color_setting "$profile_uuid" "palette" "$color_array"

echo "Color settings updated successfully!"
```


here is the ai generated bash script for reading a color.txt palette dynamically :

```shell
#!/bin/bash

# Function to convert rgb(r, g, b) to hex format
rgb_to_hex() {
    # Extract numbers from rgb(r, g, b) format
    rgb=$1
    numbers=$(echo $rgb | grep -o '[0-9]\+')
    r=$(echo "$numbers" | sed -n '1p')
    g=$(echo "$numbers" | sed -n '2p')
    b=$(echo "$numbers" | sed -n '3p')
    
    # Convert to hex
    printf "#%02X%02X%02X" "$r" "$g" "$b"
}

# Function to get the profile UUID
get_profile_uuid() {
    # First try the Mint/Cinnamon specific path
    local uuid=$(gsettings get org.gnome.Terminal.ProfilesList default | tr -d "'")
    
    if [ -z "$uuid" ]; then
        # If that fails, try getting list of profiles
        local profile_list=$(gsettings get org.gnome.Terminal.ProfilesList list)
        # Get the first profile from the list if it exists
        uuid=$(echo "$profile_list" | grep -o "'[^']*'" | head -1 | tr -d "'")
    fi
    
    if [ -z "$uuid" ]; then
        # If still no UUID found, check alternative location
        uuid=$(dconf list /org/gnome/terminal/legacy/profiles:/ | grep '^:' | head -1 | tr -d '/:')
    fi

    echo "$uuid"
}

# Function to update color setting
update_color_setting() {
    local profile_uuid=$1
    local setting_name=$2
    local color_value=$3
    
    # Try gsettings first
    gsettings set "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile_uuid/" "$setting_name" "$color_value"
    
    # If gsettings fails, try dconf
    if [ $? -ne 0 ]; then
        dconf write "/org/gnome/terminal/legacy/profiles:/:$profile_uuid/$setting_name" "'$color_value'"
    fi
}

# Check if file is provided
if [ $# -ne 1 ]; then
    echo "Usage: $0 <color_file>"
    echo "File should contain 18 colors in rgb(r,g,b) format, one per line:"
    echo "Line 1: foreground color"
    echo "Line 2: background color"
    echo "Lines 3-18: palette colors"
    exit 1
fi

# Check if file exists
if [ ! -f "$1" ]; then
    echo "Error: File $1 does not exist"
    exit 1
fi

# Get the profile UUID
profile_uuid=$(get_profile_uuid)
if [ -z "$profile_uuid" ]; then
    echo "Error: Could not find terminal profile UUID"
    exit 1
fi

echo "Found profile UUID: $profile_uuid"

# Read all colors
mapfile -t colors < "$1"

# Check if we have exactly 18 colors
if [ ${#colors[@]} -ne 18 ]; then
    echo "Error: Expected 18 colors, but found ${#colors[@]}"
    echo "Format should be: foreground, background, followed by 16 palette colors"
    exit 1
fi

# Convert and set foreground color
foreground=$(rgb_to_hex "${colors[0]}")
echo "Setting foreground color to $foreground"
update_color_setting "$profile_uuid" "foreground-color" "$foreground"

# Convert and set background color
background=$(rgb_to_hex "${colors[1]}")
echo "Setting background color to $background"
update_color_setting "$profile_uuid" "background-color" "$background"

# Process palette colors (remaining 16 colors)
palette_colors=()
for i in {2..17}; do
    hex=$(rgb_to_hex "${colors[$i]}")
    palette_colors+=("'$hex'")
done

# Set the palette
color_array="[$(IFS=,; echo "${palette_colors[*]}")]"
echo "Setting color palette"
update_color_setting "$profile_uuid" "palette" "$color_array"

echo "Color settings updated successfully!"
```



