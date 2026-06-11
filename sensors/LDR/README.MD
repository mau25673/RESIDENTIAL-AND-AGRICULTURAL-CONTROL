# LDR
<div align="center">
  <img src="https://cdn.awsli.com.br/600x700/468/468162/produto/19414320323d30eb14.jpg" alt="LDR" width="250"/>
  <h3></h3>
</div>

LDR stands for Light Dependent Resistor, an electric component which lowers its electric resistance the brighter the ambient light gets.
It is simple to use and cheap, working in most environments.

For how it must be connected, follow this diagram:
<div align="center">
  <img src="https://europe1.discourse-cdn.com/arduino/original/4X/0/2/f/02fce68c34e1c26ee73aefac380e3dd772d3f5b2.jpeg" alt="LDR connection" width="250"/>
  <h3></h3>
</div>
Connect one end to a power output (3.3V on ESP32), and the other end to the analog input which you will use, while also connecting a 10kΩ resistor between 
the analog input and the GND.

As the LDR reading has no direct measure, the best way to read it is to use the analogRead() function, which returns a value from 0 to 4095 in ESP32, 
the lower, the darker.

Here's an example code:
```cpp
// Pin definitions
const int ldrPin = 34;       // Analog pin GPIO 34 on the ESP32
const int ledPin = 2;        // Built-in LED on most ESP32 boards (GPIO 2)

// Darkness threshold (Adjust this based on your room's lighting)
// Since the ESP32 goes up to 4095, a value below 1500 usually indicates dark
const int darkThreshold = 1500; 

void setup() {
  Serial.begin(115200);       // ESP32 uses a standard speed of 115200 baud
  pinMode(ledPin, OUTPUT);    // Set the LED pin as an output
}

void loop() {
  // Read the voltage from the LDR circuit (returns a value from 0 to 4095)
  int lightLevel = analogRead(ldrPin); 
  
  // Print the value to the Serial Monitor
  Serial.print("Light Level: ");
  Serial.println(lightLevel);
  
  // Check if it is dark
  if (lightLevel < darkThreshold) {
    digitalWrite(ledPin, HIGH); // Turn the LED ON
  } else {
    digitalWrite(ledPin, LOW);  // Turn the LED OFF
  }
  
  delay(200); // Wait 200 milliseconds before the next reading
}
```
Expected result:
```text
Light Level: x
```
And the built-in led will turn on if the room is dark enough, otherwise, it won't turn on.
