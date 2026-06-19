# EndStop Sensor
<div align="center">
  <img src="https://acdn-us.mitiendanube.com/stores/033/056/products/sensor-de-fim-de-curso-mecanico-com-plug-cabo-70cm-para-impressora-3d1-6a3b69e67f3778609516122011861754-1024-1024.webp" alt="EndStop Sensor" width="400"/>
  <h3></h3>
</div>

The Mechanical Endstop Sensor is a widely used limit switch solution in 3D printers. It features a microswitch with a metal lever that physical components press against to determine position limits or establish
the reference point.

Unlike optical alternatives, it relies on direct physical contact to complete an electrical circuit. This specific module comes on a small breakout board, often equipped with status LEDs and pre-wired connector 
headers to ensure a clean interface with control boards like RAMPS or CNC Shields.

It can operate at 3.3V or 5V and provides:

- Signal Output (SIG): Changes logic state (typically switches to LOW or GND) when the metal lever is pressed;
- Status Indicator: An onboard LED that provides immediate visual confirmation when the mechanical switch is triggered.

For connections, this Mechanical Endstop module features 3 pins:

<div align="center">
  <img src="https://fabricadebolso.com.br/wp-content/uploads/2026/06/K00AD49_05.jpg" alt="EndStop Sensor Connections" width="400"/>
  <h3></h3>
</div>

- VCC (Red cabble): supplies power for the onboard indicator LED;
- GND (Black cabble): provides the common ground connection;
- SIGNAL (Green cabble): outputs the logic state to the microcontroller.

Here is a code for testing:
```cpp
int endstopPin = 18;  // SIGNAL pin connected to digital pin 2

void setup() {
  // Start serial communication for monitoring
  Serial.begin(9600);

  // Configure the digital pin as input with internal pull-up resistor
  pinMode(endstopPin, INPUT_PULLUP);
  Serial.println("Mechanical Endstop Sensor Test");
}

void loop() {
  // Read digital value of the sensor
  int endstopState = digitalRead(endstopPin);

  // Print the sensor reading
  Serial.print("Sensor State: ");
  Serial.print(endstopState);

  // Check the digital output (Active LOW when pulled up internally)
  if (endstopState == LOW) {
      Serial.print(" -> Endstop Pressed!");
  } else {
      Serial.print(" -> Endstop Released.");
  }
  
  Serial.println();

  // Wait 200 milliseconds between measurements
  delay(200);
}
```

Expected result:
```text
Mechanical Endstop Sensor Test
Sensor State: 1 -> Endstop Open (Released).
```
