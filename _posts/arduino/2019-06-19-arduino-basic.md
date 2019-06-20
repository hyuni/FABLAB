---
title: "Arduino Basic"
categories:
  - Arduino
tags:
  - Arduino
---

# Arduino Basic

### LED 점멸

  ```arduino
  void setup() {
    // put your setup code here, to run once:
    pinMode(13, OUTPUT);
  }

  void loop() {
    // put your main code here, to run repeatedly:
    digitalWrite(13, HIGH);
    delay(1000);

    digitalWrite(13, LOW);
    delay(1000);
  }
  ```


### 초록, 노랑, 빨강 LED 점멸

```arduino
void setup() {
  // put your setup code here, to run once:
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
}

void loop() {
  // 초록 LED - On, 노랑 빨강 LED - Off
  digitalWrite(11, HIGH);
  digitalWrite(12, LOW);
  digitalWrite(13, LOW);

  delay(5000);

  // 노랑 LED - 1초에 두번 점멸, 초록 빨강 LED - Off
  for(int i=1; i <= 2; i++) {
    digitalWrite(11, LOW);
    digitalWrite(12, HIGH);
    digitalWrite(13, LOW);
    delay(500);

    digitalWrite(11, LOW);
    digitalWrite(12, LOW);
    digitalWrite(13, LOW);
    delay(500);  
  }

  // 빨강 LED - ON, 초록 노랑 LED - Off
  digitalWrite(11, LOW);
  digitalWrite(12, LOW);
  digitalWrite(13, HIGH);
  delay(5000);
}
```
