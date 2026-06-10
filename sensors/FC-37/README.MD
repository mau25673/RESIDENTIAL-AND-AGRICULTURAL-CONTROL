# FC-37 (Rain Sensor)
<div align="center">
  <img src="https://d229kd5ey79jzj.cloudfront.net/891/images/891_1_H.png" alt="FC-37 Rain Sensor" width="400"/>
  <h3></h3>
</div>

The FC-37 is a low-cost rain detection sensor used in IoT and automation projects. It can detect the presence of water on its sensing surface by measuring changes in electrical conductivity between exposed conductive tracks.

The sensor is commonly sold together with an LM393 comparator module, which provides both analog and digital outputs, making it easy to interface with microcontrollers such as [ESP32].

It uses an operating voltage of 3.3V to 5V and provides:
- Analog Output (AO): Indicates the amount of water detected on the sensor surface;
- Digital Output (DO): Indicates whether the detected water level exceeds the threshold set by the onboard potentiometer.

For connections, the FC-37 sensing plate has 2 pins and the LM393 module has 4 pins:
<div align="center">
  <img src="https://how2electronics.com/wp-content/uploads/2023/12/RainDrop-Sensor-Pinout.jpg" alt="FC-37 pinout" width="400"/>
  <h3></h3>
</div>

Where:
- VCC must be connected to a 3.3V or 5V power source;
- GND must be connected to ground;
- AO provides the analog signal;
- DO provides a digital signal.

When water droplets fall on the sensing plate, the resistance between the conductive tracks decreases, causing a change in the output signals that can be read by the microcontroller.

Here is a code for testing:

```cpp
// Declare variables for both, analog and digital output
int rainAnalogPin = A0;  // AO
int rainDigitalPin = 2;  // DO

void setup() {
  // Start serial communication for monitoring
  Serial.begin(9600);

  // Configure the digital pin as input
  pinMode(rainDigitalPin, INPUT);
  Serial.println("FC-37 Rain Sensor Test");
}

void loop() {
  // Read analog value of the sensor
  int analogValue = analogRead(rainAnalogPin);
  
  // Read digital value of the sensor
  int digitalValue = digitalRead(rainDigitalPin);

  // Print both sensor readings
  Serial.print("Analog Value: ");
  Serial.print(analogValue);
  Serial.print(" | Digital Value: ");
  Serial.print(digitalValue);

  // Check the digital output
  if (digitalValue == LOW) {
      Serial.print(" -> Rain detected!");
  } else {
      Serial.print(" -> No rain detected.");
  }
  
  Serial.println();

  // Wait 1 second between measurements
  delay(1000);
}
```

Expected result:
```text
FC-37 Rain Sensor Test
Analog Value: 1023 | Digital Value: 1 -> No rain detected.
```
