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
