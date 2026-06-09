# Gas-leak-Alarm-system

A gas leakage detection system using ESP32, MQ2 sensor, LED, and buzzer.

## Features

- Detect gas levels using MQ2 sensor
- LED status indication
- Warning buzzer alerts
- Emergency alarm system
- Serial monitor readings

## Components

- ESP32
- MQ2 Gas Sensor
- LED
- Buzzer

## gas readings 

Gas < 1500 → NORMAL  

1500–2499 → WARNING  

2500+ → EMERGENCY  

## project code

```cpp
#define MQ2_PIN 34
#define LED_PIN 23
#define BUZZER_PIN 19

void setup() {
  Serial.begin(115200);

  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(LED_PIN, LOW);
  noTone(BUZZER_PIN);
}

void loop() {

  int gas = analogRead(MQ2_PIN);

  Serial.print("Gas Value: ");
  Serial.println(gas);

  if (gas < 1500) {

    digitalWrite(LED_PIN, LOW);
    noTone(BUZZER_PIN);

    Serial.println("NORMAL");
  }

  else if (gas >= 1500 && gas < 2500) {

    digitalWrite(LED_PIN, HIGH);

    tone(BUZZER_PIN, 1000);
    delay(200);
    noTone(BUZZER_PIN);

    Serial.println("WARNING");
  }

  else {

    digitalWrite(LED_PIN, HIGH);

    tone(BUZZER_PIN, 1500);

    Serial.println("EMERGENCY");
  }

  delay(500);
}
~~~


