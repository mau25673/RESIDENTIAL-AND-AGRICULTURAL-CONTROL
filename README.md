# Residential and Agricultural Control Interface with IoT

<div align="center">
  <img src="https://i.imgur.com/5leh4PJ.png" alt="Esquematic from circuit" width="600"/>
  <h3></h3>
</div>

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

**Authors:** Maurício Melo Filho and Thales Soares de Araújo.

---

## About the Project

This project implements a low-cost, expandable structure for residential and agricultural control, using Home Assistant OS running in a Raspberry Pi and ESPHome for communication between the main server and the ESP32s that handle the reading of different sensors and activation of peripherals, providing information, automation and control to many different use cases. The system can be controlled from long distances using Tailscale as a VPN (Virtual Private Network), connecting a cellphone directly to the Home Assistant Supervisor without relying on being in the same wifi network.

---

## Minimum Required Hardware and Software

### Hardware
- 1x Raspberry Pi 3 (or newer, at least Raspberry Pi 4 is recommended) with Home Assistant OS.
- 1x ESP32 microcontroller (development board).
- Micro-USB data capable cable for programming the ESP32 and powering it.

### Software
- CP2102 USB to UART Bridge Controller Driver (required for most ESP32 boards).

## Recommended for basic implementation
> Note: The recommended for basic implementation section mentions which components where used in the test implementation.
### Hardware
- 2x 10kΩ resistors.
- 1x DHT22 sensor.
- 1x LDR sensor.
- 1x FC-37 sensor.
- 1x Endstop sensor.
- Jumper cables.

---

## Installation and Configuration

### Step 1: Install Home Assistant on the Raspberry Pi
1. **Prepare the OS**  
   Use Raspberry Pi Imager to install *Home Assistant* on a MicroSD card.
2. **Boot the System**  
   Check to see if everything went smoothly, by either a monitor or following the next steps directly.

---

### Step 2: Open the Supervisor and Install ESPHome Add-on
1. **Connect the Raspberry Pi to the Internet**  
   This can be done either by connecting it directly by an ethernet cable or through Wi-Fi, through the following command:
   ```sh
   network update wlan0 --ipv4-method auto --ipv6-method auto --wifi-auth wpa-psk --wifi-mode infrastructure --wifi-ssid <Your_WiFi_SSID> --wifi-psk <Your_WiFi_Password>
   ```

3. **Open the Supervisor**  
   On a web browser connected to the same network as the Raspberry Pi, open the following URL:
   ```sh
   http://homeassistant.local:8123/
   ```  
   It should take some time for it to finish booting up completely, so wait a few minutes after powering it before connecting to the supervisor.
