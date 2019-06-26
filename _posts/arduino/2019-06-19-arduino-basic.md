---
title: "Arduino Basic"
categories:
  - Arduino
tags:
  - Arduino
---

# Arduino Basic

### 기본 함수
1. setup 함수
2. loop 함수
3. pinMode 함수
4. digitalWrite 함수
5. analogRead/Write 함수
6. delay 함수
7. Serial 관련 함수(begin, print, println 등)

### PWM(Plus with Modulation ; 펄스 폭 변조)

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

### PWM 으로 LED 밝기 조절

```arduino
int LED1 = 10;
int LED2 = 11;

int delayTime = 200;

void setup() {
  // put your setup code here, to run once:
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:

  for(int count = 0; count <= 255; count += 2) {
    analogWrite(LED1, 0);
    analogWrite(LED2, 0);
    delay(delayTime);

    analogWrite(LED1, count);
    analogWrite(LED2, count);
    delay(delayTime);
  }

  delay(1000);
}
```


### RGB LED 제어
```arduino
int RED = 9;
int GREEN = 10;
int BLUE = 11;

int delayTime = 500;

void setup() {
  // put your setup code here, to run once:
  pinMode(RED, OUTPUT);
  pinMode(GREEN, OUTPUT);
  pinMode(BLUE, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  analogWrite(RED, 0);
  analogWrite(GREEN, 0);
  analogWrite(BLUE, 0);

  for(int nLED = RED; nLED <= BLUE; nLED++) {
    analogWrite(RED, random(256));
    analogWrite(GREEN, random(256));
    analogWrite(BLUE, random(256));
    delay(500);

    analogWrite(RED, 0);
    analogWrite(GREEN, 0);
    analogWrite(BLUE, 0);
    delay(500);
  }
}
```


### 포토드랜지스터 화재감지기
```arduino
int flame = A0;
int buzzer = 13;
int val = 0;

void setup() {
  // put your setup code here, to run once:
  pinMode(buzzer, OUTPUT);
  pinMode(flame, INPUT);
  Serial.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedly:
  val = analogRead(flame);
  Serial.println(val);

  if (val >= 900) {
    digitalWrite(buzzer, HIGH);
    Serial.println("High");
    //tone(buzzer, 1000, 500);
  } else {
    digitalWrite(buzzer, LOW);
    Serial.println("LOW");
  }

  delay(100);
}
```
