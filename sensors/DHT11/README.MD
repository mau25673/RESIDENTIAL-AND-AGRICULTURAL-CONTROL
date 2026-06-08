# DHT11
<div align="center">
  <img src="https://d229kd5ey79jzj.cloudfront.net/791/images/791_1_H.png" alt="DHT 11" width="250"/>
  <h3></h3>
</div>

DHT11 is an easy to use digital temperature and humidity sensor, commonly used in IoT projects like this one, providing information with a good precision at a 
cheap price, with a pre-made library that facilitates the implementation.
It uses a operating voltage of 3.3V to 5V and a operating current of 2.5mA.
Its reading range is:
- 0°C to 50°C (Precision of ±2°C);
- 20% to 90% RH (Precision of 5% RH).

For data pins we have the bare sensor (4 pins) and the module (3 pins):
<div align="center">
  <img src="https://europe1.discourse-cdn.com/arduino/original/4X/4/1/c/41c4c8c991e93c81c638564d369848a666401575.jpeg" alt="DHT 11 data pins" width="400"/>
  <h3></h3>
</div>
Where VCC must be connected to a power output between 3.3V and 5V, GND to ground, and DATA to the pin which will be receive the signal in your ESP32.
When using the bare sensor, connect a 10kΩ pull-up resistor between the VCC and DATA lines.

Here is a code for testing:

```cpp
#include "DHT.h"

// Define the digital pin connected to the DHT11 data pin, in this example it is the second one.
#define DHTPIN 2     

// Define the sensor type (DHT11 or DHT22)
#define DHTTYPE DHT11   

// Initialize the DHT sensor
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  // Start serial communication for monitoring
  Serial.begin(9600);
  Serial.println("DHT11 Sensor Test");

  // Initialize the sensor
  dht.begin();
}

void loop() {
  // Wait 2 seconds between measurements
  delay(2000);

  // Read humidity (%)
  float h = dht.readHumidity();
  
  // Read temperature in Celsius (default)
  float t = dht.readTemperature();
  
  // Read temperature in Fahrenheit (isFahrenheit = true)
  float f = dht.readTemperature(true);

  // Check if any reads failed and exit early to try again
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  // Print results to the Serial Monitor
  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print("%  |  ");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print("°C / ");
  Serial.print(f);
  Serial.println("°F");
}```
Expected result:
```text
Humidity: x% | Temperature: x°C / x°F
```
