## Expanding the ESP32 with Additional Sensors
ESPHome allows the ESP32 to be expanded with virtually any supported sensor by simply connecting the hardware and editing the device's .yaml configuration. After uploading the new configuration, Home Assistant will automatically detect the new entities.

### Step 1: Connect the New Sensor

Before editing the software, connect the new sensor to the ESP32.

1. Check the sensor documentation
- Verify the operating voltage (3.3 V or 5 V).
- Identify the communication protocol:
   - GPIO (Digital);
   - Analog (ADC);
   - I²C;
   - SPI;
   - UART;
   - OneWire;
2. Connect the sensor
- Connect the sensor to the correct ESP32 pins according to its datasheet.

### Step 2: Add the Sensor to the YAML File
Open the ESPHome dashboard and click Edit on your device. Locate the appropriate section of the .yaml file and add the new sensor configuration.

For example, a DHT22 temperature and humidity sensor:

```
sensor:
  - platform: dht
    pin: GPIO4
    model: DHT22
    temperature:
      name: "Room Temperature"
    humidity:
      name: "Room Humidity"
    update_interval: 10s
```

Or an analog soil moisture sensor:

```
sensor:
  - platform: adc
    pin: GPIO34
    name: "Soil Moisture"
    update_interval: 5s
```

### Step 3: Validate the Configuration
Before installing the firmware, click Validate. ESPHome will compile the configuration and report any syntax or compatibility errors.

If no errors are found, continue with the installation.

### Step 4: Upload the New Firmware

Follow the steps in [Basic Setup](Basic_Setup.md) to upload and run the update code.

### Step 5: Verify the New Entities in Home Assistant

After the ESP32 reconnects to the network: Open Home Assistant. Navigate to:
Settings → Devices & Services → ESPHome
Select your ESP32. The new entities should automatically appear.

If they do not, click Reload or restart the ESPHome device.

## Components Yaml Setup:
### Binary Sensors
Binary sensors represent only two possible states:
ON / OFF
True / False
Open / Closed

Example:
```
binary_sensor:
  - platform: gpio
    pin: GPIO18
    name: "Door Sensor"
```

### Analog Sensors
Analog sensors output a voltage proportional to the measured value.

Example:
```
sensor:
  - platform: adc
    pin: GPIO34
    name: "Water Level"
```

### Output
#### Relay
```
switch:
  - platform: gpio
    pin: GPIO23
    name: "Water Pump"
```

#### PWM
```
output:
  - platform: ledc
    pin: GPIO19
    id: pwm_output
```

#### Buzzer
```
output:
  - platform: ledc
    pin: GPIO25
    id: buzzer
```

## Finding New Components

ESPHome supports hundreds of devices, and new integrations are added frequently. The complete list of supported components can be found in the official documentation:
- https://esphome.io/components/
- https://devices.esphome.io/

Before adding a new sensor, check its documentation page to verify:
- Supported ESPHome platform.
- Required libraries.
- Wiring diagram.
- Required communication protocol.
- Example YAML configuration.
