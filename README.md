# Residential and Agricultural Control Interface with IoT

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

**Authors:** Maurício Melo Filho and Thales Soares de Araújo.

---

## About the Project

This project implements a low-cost, expandable structure for residential and agricultural control, using Home Assistant OS running in a Raspberry Pi and ESPHome for communication between the main server and the ESP32s that handle the reading of different sensors and activation of peripherals, providing information, automation and control to many different use cases. The system can be controlled from long distances using Tailscale as a VPN (Virtual Private Network), connecting a cellphone directly to the Home Assistant Supervisor without relying on being in the same Wi-Fi network.

---

## Features  

- **Web Control Dashboard:** Dashboard for controlling your peripherals and the ambient in which they are installed.
- **Easy to Use and Modify:** Using pre-made add-ons for Home Assistant, it can be modified and expanded and customized without coding experience.
- **Low Cost:** Implemented using low-end hardware and affordable peripherals with open-source software.

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

## Hardware Installation

### ESP32 and Peripherals

<div align="center">
  <img src="https://i.imgur.com/44zt0wd.png" alt="Esquematic from circuit" width="600"/>
  <h3></h3>
</div>

As shown in the image above, the ESP32 should be connected to the peripherals used for it to work correctly. GPIO pins may be changed if you wish to, but the .yaml configuration which ESPHome will run must be changed to follow the changes.

### Hardware Connections
#### DHT22:
The DHT22 is a digital temperature and humidity sensor. Detailed specifications can be found in the [DHT22 documentation](/sensors/DHT22/README.md).

| Recommended GPIO / Pin | Function | Description |
| :--- | :--- | :--- |
| **VCC (3.3V)** | Power Supply | Powers the sensor. |
| **GPIO 4** | Data Signal | Data transmission (requires a 10kΩ pull-up resistor to 3.3V). |
| **NC** | Not Connected | This pin has no electrical connection. |
| **GND** | Ground | Ground connection for the sensor. |

#### FC-37:
The FC-37 is a rain and raindrop detection sensor. Detailed specifications can be found in the [FC-37 documentation](/sensors/FC-37/README.MD).

| Recommended GPIO / Pin | Function | Description |
| :--- | :--- | :--- |
| **VCC (3.3V)** | Power Supply | Powers the sensor. |
| **GND** | Ground | Ground connection for the sensor. |
| **GPIO 34 (AO)** | Analog Output | Connects to the Analog Output (AO) of the sensor for real-time rain intensity readings. |
| **GPIO 37 (DO)** | Digital Output | Connects to the Digital Output (DO) of the sensor for binary rain detection (Rain / No Rain), adjustable via potentiometer. |

#### LDR (Photoresistor):
The LDR (Photoresistor) is a light-dependent resistor used to measure ambient light levels. Detailed specifications can be found in the [LDR documentation](/sensors/LDR/README.MD).

| Recommended GPIO / Pin | Function | Description |
| :--- | :--- | :--- |
| **VCC (3.3V)** | Power Supply | Powers the voltage divider circuit. |
| **GPIO 32 (ADC)** | Analog Input | Connects to the analog pin to read varying voltage levels based on light intensity. |
| **GND** | Ground | Ground connection for the circuit. |

This section details the connection of a DC Motor controlled via an SRD-05VDC-SL-C relay module, with voltage regulation supplied by an MT3608 step-up converter. Detailed specifications can be found in the [Motor & Power documentation](/sensors/motor-relay/README.md).

#### Relay Module:
| Recommended GPIO / Pin | Function | Description |
| :--- | :--- | :--- |
| **VCC (5V)** | Power Supply | Powers the relay electromagnet coil. |
| **GND** | Ground | Ground connection for the circuit. |
| **GPIO 12 (IN)** | Control Signal | Digital output pin to trigger the relay. |

#### Power & Motor:
| Component / Pin | Connected To | Description |
| :--- | :--- | :--- |
| **MT3608 VIN+** | Main Power Source | Input voltage from the main power supply. |
| **MT3608 VIN-** | Main Power Ground | Ground connection from the main power supply. |
| **MT3608 VOUT+** | Relay COM (Common) | Elevated voltage output adjusted via the MT3608 potentiometer to match the motor's operating voltage (12V). |
| **MT3608 VOUT-** | Motor (-) Terminal | Direct ground path for the motor power circuit. |

## Software Installation and Configuration

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

2. **Open the Supervisor**  
   On a web browser connected to the same network as the Raspberry Pi, open the following URL:
   ```sh
   http://homeassistant.local:8123/
   ```
   It should take some time for it to finish booting up completely, so wait a few minutes after powering it before connecting to the supervisor.

3. **Create an User**  
   After succesfully opening the supervisor, a user must be created to be able to make use of the supervisor and control de Home Assistant supervisor.

4. **Install ESPHome Add-on**  
   In a computer connected to the same network as Home Assistant, open this link: https://my.home-assistant.io/redirect/supervisor_addon/?addon=5c53de3b_esphome&repository_url=https%3A%2F%2Fgithub.com%2Fesphome%2Fhome-assistant-addon  
   It will open a screen showing ESPHome add-on store's page, click on install, and check for it to open automatically.
   > Note: If you need more information to complete this step, it can be found in this guide: https://esphome.io/guides/getting_started_hassio/

---

### Step 3: Setting up ESPHome in the ESP32 microcontroller
1. **Creating a device**  
   Click on the "New Device" button in the bottom-right corner of the screen, where it will ask for Wi-Fi connection details before proceeding. Choose ESP32,
   then continue through the wizard to complete the installation. If this is the first time connecting the ESP32, you'll need a physical connection, which is
   where the micro-USB data cable will be used. Connect it to the ESP32, then click the three dot menu in the device you created and choose "Install", then choose
   install through direct connection with the supervisor computer.
   > Note: If you're using a Raspberry Pi with 1 GB of RAM, it won't be powerful enough to compile the .yaml file needed to configure the ESP32. You'll need to compile it in your own machine for it to work. A more in-depth tutorial can be found [here.](./tutorials/Compiling_ESPHome.md)

2. **Uploading the .yaml Code to the ESP32**
   
