# ESP-32
<div align="center">
  <img src="https://joy-it.net/files/files/Produkte/SBC-NodeMCU-ESP32-C/SBC-NodeMCU-ESP32-C_01.png" alt="Esp-32" width="400"/>
  <h3></h3>
</div>

The ESP32 is a powerful, low-cost microchip system-on-a-chip (SoC) with integrated Wi-Fi and dual-mode Bluetooth. Designed primarily for Internet of Things (IoT) and smart home automation projects, 
it features a dual-core processor that delivers significantly higher performance than traditional microcontrollers.

It is highly versatile, operating at a high clock speed and featuring advanced power-management modes, making it ideal for everything from wearable electronics to complex industrial monitoring systems.

## Electrical Specifications

- **Operating Voltage (Chip):** 3.3V;
- **Input Voltage (VIN/5V Pin):** 5V DC (regulated down to 3.3V by the onboard AMS1117 regulator);
- **Max Current per GPIO Pin:** 40 mA;
- **Max Total Current:** 1200 mA.

## Core Performance & Connectivity

- **Processor:** Tensilica Xtensa Dual-Core 32-bit LX6;
- **Clock Frequency:** Up to 240 MHz;
- **Internal Memory:** 520 KB SRAM;
- **External Storage (Flash):** 8 MB;
- **Wireless Protocols:** 2.4 GHz Wi-Fi & Bluetooth v4.2.

##  GPIO Reference Table (Crucial for ESPHome setup)

Not all ESP32 pins behave the same way. Some pins pulse during startup, while others lack essential features. Use this quick reference guide when assigning pins in your YAML file:

| GPIO Pins | Recommended Usage |
| :--- | :--- |
| **4, 13, 14, 16, 17, 18, 19, 21, 22, 23, 25, 26, 27, 32, 33** | General purpose |
| **34, 35, 36, 39** | Digital or analog inputs only (No internal pull-up) |
| **0, 2, 5, 12, 15** | Boot configuration pins (Avoid using for sensors) |
| **6, 7, 8, 9, 10, 11** | Connected to internal flash memory (Do not use) |
