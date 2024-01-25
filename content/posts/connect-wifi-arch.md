+++
title = 'Connect to Wifi during Arch installation'
date = 2024-01-25T00:13:08-06:00
draft = false
+++

Hello Reader,

During the Arch Linux installation process, connecting to WiFi might be necessary if you are not using a wired connection. Here's a step-by-step guide to help you get your Arch system connected to WiFi.

### Check Available Interfaces
First, check the available wireless interfaces using the following command:

```bash
iwconfig
```

### Restart DHCP Service
Restart the DHCP service to ensure that it is ready to configure the network interfaces:

```bash
systemctl restart dhcpcd
```

### Scan for WiFi Networks
Use the following command to scan for available WiFi networks:

```bash
iwlist <interface> scan
```

Replace `<interface>` with the name of your wireless interface.

### Create WPA Supplicant Configuration
Generate a WPA Supplicant configuration file for your WiFi network. Replace `<SSID>` and `<PSK>` with your WiFi network's SSID and passphrase:

```bash
wpa_passphrase "<SSID>" "<PSK>" > /etc/wpa_supplicant/wpa_supplicant-<interface>.conf
```

### Connect to WiFi
Initiate the connection to your WiFi network using the generated configuration file:

```bash
wpa_supplicant <interface> -c /etc/wpa_supplicant/wpa_supplicant-<interface>.conf
```

### Obtain IP Address
Finally, obtain an IP address for your wireless interface using DHCP:

```bash
dhclient <interface>
```

### Verify Connection
Ensure that your Arch Linux system is connected to the internet by pinging a reliable server, for example, Google:

```bash
ping google.com
```

If you receive responses, congratulations! Your Arch Linux system is now connected to WiFi.

Remember to replace `<interface>`, `<SSID>`, and `<PSK>` with your actual wireless interface name, WiFi network SSID, and passphrase. This should help you seamlessly connect to WiFi during the Arch Linux installation process.

Cheers,

Anson Sarosh Dsouza