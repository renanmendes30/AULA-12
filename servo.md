```
#include <Servo.h>
Servo servo;
char comando;

void setup() {
  servo.attach(9);
  Serial.begin(9600);   // mesma velocidade do Python
  pinMode(13, OUTPUT);  // LED (pino 13)
}

void loop() {
  if (Serial.available() > 0) {
    comando = Serial.read();

    if (comando == 'l') {
      digitalWrite(13, HIGH);  // liga LED
      servo.write(90);
      Serial.println("LED LIGADO");
    }

    else if (comando == 'd') {
      digitalWrite(13, LOW);   // desliga LED
      servo.write(180);
      Serial.println("LED DESLIGADO");
    }
  }
}
```
