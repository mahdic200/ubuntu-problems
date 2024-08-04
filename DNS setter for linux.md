navigate to your `~/.local/bin` folder :

```shell
cd ~/.local/bin
```

then make two files named `nson` and `nsoff` respectively :

```shell
touch nson nsoff
```

then give them permission to become executable :

```shell
chmod +x nson nsoff
```


# nson file content

```bash
#!/bin/bash

# Variables for DNS addresses
DNS1="185.51.200.2"
DNS2="178.22.122.100"

# Get the name of the WiFi interface
WIFI_INTERFACE=$(nmcli device status | grep wifi | awk '{print $1}')

# Get the name of the active WiFi connection
WIFI_CONNECTION=$(nmcli -t -f active,ssid dev wifi | grep '^yes' | cut -d: -f2)

# Set the DNS for the WiFi connection
nmcli con mod "$WIFI_CONNECTION" ipv4.dns "$DNS1 $DNS2"
nmcli con mod "$WIFI_CONNECTION" ipv4.ignore-auto-dns yes

# Restart the network connection to apply changes
nmcli con down "$WIFI_CONNECTION" && nmcli con up "$WIFI_CONNECTION"

echo "DNS for WiFi connection '$WIFI_CONNECTION' set to $DNS1 and $DNS2."

```

# nsoff file content

```bash
#!/bin/bash

# Get the name of the WiFi interface
WIFI_INTERFACE=$(nmcli device status | grep wifi | awk '{print $1}')

# Get the name of the active WiFi connection
WIFI_CONNECTION=$(nmcli -t -f active,ssid dev wifi | grep '^yes' | cut -d: -f2)

# Clear the DNS settings for the WiFi connection
nmcli con mod "$WIFI_CONNECTION" ipv4.dns ""
nmcli con mod "$WIFI_CONNECTION" ipv4.ignore-auto-dns no

# Restart the network connection to apply changes
nmcli con down "$WIFI_CONNECTION" && nmcli con up "$WIFI_CONNECTION"

echo "DNS settings for WiFi connection '$WIFI_CONNECTION' have been cleared."

```