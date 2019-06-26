---
title: "Arduino Basic"
categories:
  - Arduino
tags:
  - Arduino, 플로팅현상, 풀업 저항, 풀다운 저항, INPUT_PULLUP, 온습도센서, DHT11, LiquidCrystal, LCD, RTC, DS1302
---

# Arduino Basic #2

### 알아야 할 사항

1. 플로팅 현상
   - 스위치 열러있는 경우 전류가 흐르지 않아 0, 1 사이를 방황하는 상태
   - 스위치 닫혀있는 경우는 정상적이 됨
   - 참고 : [플로팅 상태](https://kocoafab.cc/tutorial/view/526)

2. 플로팅 현상을 없애는 방법
   * 풀업 저항
     - 스위치 ON 에서는 0, OFF 상태에서는 1 이 되도록 회로 구성

     - 풀업 저항 아두이노 구성![풀업 저항](http://kocoafab.cc/data/201510051616294525.png)

     - 풀업 회로도 - Switch OFF ![풀업 Switch OFF 회로도](http://kocoafab.cc/data/201510051626173888.jpg)

     - 풀업 회로도 - Switch ON ![풀업 Switch ON 회로도](http://kocoafab.cc/data/201510051641337951.jpg)


   * 풀다운 저항
     - 스위치 ON 에서는 1, OFF 상태에서는 0 이 되도록 회로 구성

     - 풀다운 저항 아두이노 구성 ![풀다운 저항](http://kocoafab.cc/data/201608191437381120.png)

     - 풀다운 회로도 - Switch OFF ![풀다운 Switch OFF 회로도](http://kocoafab.cc/data/201510051724506543.jpg)

     - 풀다운 회로도 - Switch ON ![풀다운 Switch ON 회로도](http://kocoafab.cc/data/201510051729021246.jpg)



   * 코드로 없애는 방법(아두이노)

     - 아두이노에서는 자체적으로 pinMode()에서 INPUT과 OUTPUT외에도 INPUT_PULLUP이라는 소프트웨어적인 풀업모드를 제공
     - 아두이노 각 핀에는 내부 풀업 저항이 달려 있음

      ```Arduino
      int pushButton = 4;

      void setup() {
        Serial.begin(9600);
        pinMode(pushButton, INPUT_PULLUP); //INPUT_PULLUP모드 적용
      }

      void loop() {
        int buttonState = digitalRead(pushButton);
        Serial.println(buttonState);
        delay(1);    
      }
      ```

### 온습도 센서(DHT11)

```Arduino
#include <DHT11.h>

int pin=4;
DHT11 dht11(pin);

void setup() {
   Serial.begin(9600);
   while (!Serial) {
      ; // wait for serial port to connect. Needed for Leonardo only
   }
}

void loop() {
  int err;
  float temp, humi;

  if((err=dht11.read(humi, temp))==0) {
    Serial.print("temperature:");
    Serial.print(temp);
    Serial.print(" humidity:");
    Serial.print(humi);
    Serial.println();
  } else {
    Serial.println();
    Serial.print("Error No :");
    Serial.print(err);
    Serial.println();    
  }

  delay(DHT11_RETRY_DELAY); //delay for reread
}
```

### LCD(LiquidCrystal)

```Arduino
#include <DHT11.h>

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

int pin = 2;
DHT11 dht11(pin);

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);

  lcd.begin();
}

void loop() {
  // put your main code here, to run repeatedly:
  int err;
  float temp, humi;

  if((err=dht11.read(humi, temp))==0)
  {
    lcd.backlight();
    lcd.display();

    lcd.print("TEMP:   ");
    lcd.print(temp);
    lcd.setCursor(0, 1);
    lcd.print("humidity: ");
    lcd.print(humi);

    Serial.print("temperature:");
    Serial.print(temp);
    Serial.print(" humidity:");
    Serial.print(humi);
    Serial.println();
  }
  else
  {
    lcd.backlight();
    lcd.display();

    lcd.print("ERROR NO : ");
    lcd.print(err);

    Serial.println();
    Serial.print("Error No :");
    Serial.print(err);
    Serial.println();    
  }

  //delay(DHT11_RETRY_DELAY); //delay for reread
  delay(2000);
  lcd.clear();
}
```

### RTC(DS1302)

```Arduino
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Set the LCD address to 0x3F for a 16 chars and 2 line display // note: it may be different for your LCD please find it.
LiquidCrystal_I2C lcd(0x27, 16, 2);
#include <DS1302.h>

// Init the DS1302
DS1302 rtc(2, 3, 4);

// Init a Time-data structure
Time t;

void setup()
{

// Set the clock to run-mode, and disable the write protection
 rtc.halt(false);
 rtc.writeProtect(false);

 // The following lines can be commented out to use the values already stored in the DS1302
 rtc.setDOW(WEDNESDAY); // Set Day-of-Week to TUESDAY
 rtc.setTime(16, 46, 50); // Set the time to 24hr format it will automatically take time according to AM/PM
 rtc.setDate(26, 6, 2019); // Set the date to Febrauray 6th, 2018
 // initialize the LCD
 lcd.begin();
}

void loop()
{
 // Get data from the DS1302
  t = rtc.getTime();

  lcd.setCursor(0, 0);

  if (t.date<=9){
    lcd.setCursor(0,0);
    lcd.print("0");
    lcd.setCursor(1,0);
    lcd.print(t.date, DEC);
  }
  else {
    lcd.print(t.date, DEC);
  }

  lcd.setCursor(3, 0);
  lcd.print(rtc.getMonthStr());
  lcd.setCursor(12,0);
  lcd.print(t.year, DEC);
  lcd.setCursor(4,1);

  {
    if (t.hour>=12) {
      lcd.setCursor(13,1);
      lcd.print("PM");
      lcd.setCursor(4,1);
      t.hour = t.hour-12;

      if (t.hour== 0) {
      t.hour = 12; // Day 12 PM
      }

      if (t.hour<=9){
      lcd.setCursor(4,1);
      lcd.print("0");
      lcd.setCursor(5,1);
      lcd.print(t.hour, DEC);
      }
      else {
        lcd.print(t.hour, DEC);
      }
    }
    else {
      if(t.hour==0){
        t.hour=12; // Night 12 AM
      }

      lcd.setCursor(13,1);
      lcd.print("AM");
      lcd.setCursor(4,1);

      if (t.hour<=9){
        lcd.setCursor(4,1);
        lcd.print("0");
        lcd.setCursor(5,1);
        lcd.print(t.hour, DEC);
      }
      else {
        lcd.print(t.hour, DEC);
      }
    }
  }

  lcd.setCursor(6,1);
  lcd.print(":");
  lcd.setCursor(7,1);

  if (t.min<=9){
    lcd.setCursor(7,1);
    lcd.print("0");
    lcd.setCursor(8,1);
    lcd.print(t.min, DEC);
  }
  else {
    lcd.print(t.min, DEC);
  }

  lcd.setCursor(9,1);
  lcd.print(":");
  lcd.setCursor(10,1);

  if (t.sec<=9){
    lcd.setCursor(10,1);
    lcd.print("0");
    lcd.setCursor(11,1);
    lcd.print(t.sec, DEC);
  }
  else {
    lcd.print(t.sec, DEC);
  }

  delay (1000);
  lcd.clear();
}
```
