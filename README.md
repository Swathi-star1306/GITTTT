# GITTTT
FAN SPEED
```
const int tempSensorPin = A0;   
const int humiditySensorPin = A1;  

int rawValue = 0;
float voltage = 0;
float tempC = 0;
float tempF = 0;
int humidityValue = 0;

void setup() {
  Serial.begin(9600);
  pinMode(humiditySensorPin, INPUT);
}

void loop() {

 
  rawValue = analogRead(tempSensorPin);

  
  voltage = rawValue * (5000.0 / 1023.0);
  tempC = voltage / 10.0;        
  tempF = (tempC * 1.8) + 32.0;  

  Serial.print("Raw ADC = ");
  Serial.print(rawValue);

  Serial.print("\tVoltage (mV) = ");
  Serial.print(voltage, 1);

  Serial.print("\tTemperature (°C) = ");
  Serial.print(tempC, 1);

  Serial.print("\tTemperature (°F) = ");
  Serial.println(tempF, 1);
  humidityValue = analogRead(humiditySensorPin);

 
  int humidityPercent = map(humidityValue, 0, 1023, 10, 70);

  Serial.print("Humidity = ");
  Serial.print(humidityPercent);
  Serial.println("%");

  Serial.println("------------------------------------");

  delay(5000);   
}

```


PIR SENSOR
```
int buttonState = 0;

void setup()
{
  pinMode(2, INPUT);             // Button on digital pin 2
  pinMode(LED_BUILTIN, OUTPUT);  // LED on pin 13
}

void loop()
{
  buttonState = digitalRead(2);  // Read button input

  if (buttonState == HIGH)       // If button pressed
  {
    digitalWrite(LED_BUILTIN, HIGH);  // Turn LED ON
  }
  else                           // If button not pressed
  {
    digitalWrite(LED_BUILTIN, LOW);   // Turn LED OFF
  }

  delay(10);  // small delay for button stability
}

```

ULTRASONIC SENSOR

```
#define pingPin 7   // Sensor SIG pin connected to digital pin 7

long duration;
int distance;

void setup() {
  Serial.begin(9600);
}

void loop() {

  // ---- Trigger the ultrasonic burst ----
  pinMode(pingPin, OUTPUT);
  digitalWrite(pingPin, LOW);
  delayMicroseconds(2);

  digitalWrite(pingPin, HIGH);
  delayMicroseconds(10);   // Standard trigger = 10 microseconds
  digitalWrite(pingPin, LOW);

  // ---- Read echo signal ----
  pinMode(pingPin, INPUT);
  duration = pulseIn(pingPin, HIGH);   // time in microseconds

  // ---- Convert time to distance ----
  // Speed of sound = 0.0343 cm per microsecond
  distance = duration * 0.0343 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  delay(500);
}

```

GAS SENSOR

```
#include <LiquidCrystal.h>

// LCD RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  Serial.begin(9600);

  lcd.begin(16, 2);
  lcd.print("Gas Detector");

  pinMode(13, OUTPUT); // Red LED (Danger)
  pinMode(6, OUTPUT);  // Yellow LED (Warning)
  pinMode(7, OUTPUT);  // Green LED (Safe)

  delay(1000);
  lcd.clear();
}

void loop() {
  int gas_data = analogRead(A0);

  // Display gas value
  lcd.setCursor(0, 0);
  lcd.print("Gas : ");
  lcd.print(gas_data);
  lcd.print("   ");  // Extra spaces to clean leftover digits

  // -------------------------
  // GAS LEVEL DECISION LOGIC
  // -------------------------

  if (gas_data > 800) {
    // DANGER
    digitalWrite(13, HIGH); // Red LED
    digitalWrite(6, LOW);
    digitalWrite(7, LOW);

    lcd.setCursor(0, 1);
    lcd.print("DANGER !!!     ");

  } else if (gas_data > 700) {
    // WARNING
    digitalWrite(13, LOW);
    digitalWrite(6, HIGH); // Yellow LED
    digitalWrite(7, LOW);

    lcd.setCursor(0, 1);
    lcd.print("WARNING        ");

  } else {
    // SAFE
    digitalWrite(13, LOW);
    digitalWrite(6, LOW);
    digitalWrite(7, HIGH); // Green LED

    lcd.setCursor(0, 1);
    lcd.print("SAFE           ");
  }

  Serial.println(gas_data);
  delay(300);
}

```

TILT SENSOR

```
int ledPin = 13;
int inPin  = 7;

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  pinMode(inPin, INPUT);   // Reads HIGH/LOW from external input or sensor
}

void loop() {
  int val = digitalRead(inPin);   // Read pin 7

  if (val == LOW) {               // If input is LOW → LED ON
    digitalWrite(ledPin, HIGH);
  } 
  else {                          // If input is HIGH → LED OFF
    digitalWrite(ledPin, LOW);
  }

  Serial.println(val);            // Print sensor state
  delay(50);                      // Small stability delay
}

```
LDR 

```
const int LEDPin = 13;
const int LDRPin = A0;

void setup()
{
  Serial.begin(9600);
  pinMode(LEDPin, OUTPUT);
  // No need for pinMode(LDRPin, INPUT); → analogRead handles it automatically
}

void loop()
{
  int LDRStatus = analogRead(LDRPin);  // 0–1023

  Serial.print("Current Light Intensity Value: ");
  Serial.println(LDRStatus);

  if (LDRStatus <= 500)   // Dark condition
  {
    digitalWrite(LEDPin, HIGH);  // Turn ON LED
  }
  else                    // Bright condition
  {
    digitalWrite(LEDPin, LOW);   // Turn OFF LED
  }

  delay(200);   // small delay for stable readings
}

```

