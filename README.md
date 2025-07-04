# 🚗 Automatic Speed Detection & Reporting System Using Arduino

## 👩‍💻 Author: Yashomati Vasantrao Bawane

This project demonstrates a smart Arduino-based speed detection system using two IR sensors. It measures the speed of a passing vehicle and alerts the user if the speed exceeds the threshold via buzzer. The speed is displayed on an LCD in real-time.

---

## 🎯 Objective

To detect the speed of a moving vehicle using IR sensors and Arduino, and automatically alert via buzzer if overspeeding is detected. The speed is displayed on a 16x2 LCD for real-time feedback.

---

## 🔧 Hardware Used

- Arduino UNO  
- 2x IR Sensors  
- Buzzer  
- 16x2 LCD Display  
- Breadboard + Jumper Wires  
- USB Power Supply

---

## ⚙️ Working Principle

1. IR Sensor 1 detects the object and starts a timer.
2. IR Sensor 2 stops the timer once the object passes.
3. Speed is calculated based on known distance and time.
4. If speed > threshold, buzzer is activated.
5. Speed is shown on the LCD module.

---

## 💻 Code Snippet

```cpp
int sen1 = A0;
int sen2 = A3;
int ledPin = 9;
unsigned long t1 = 0;
unsigned long t2 = 0;
float velocity;
float velocity_real;
float timeFirst;
float timeScnd;
float diff;
float speedConst = 7.5;

void setup() {
  Serial.begin(9600);
  pinMode(sen1, INPUT);
  pinMode(sen2, INPUT);
  analogWrite(11, LOW);
  analogWrite(10, HIGH);
}

void loop() {
  if (analogRead(sen1) < 500 && analogRead(sen2) > 500) {
    timeFirst = millis();
    digitalWrite(ledPin, LOW);
    delay(30);
  }

  if (analogRead(sen2) > 500 && analogRead(sen1) < 500) {
    timeScnd = millis();
    diff = timeScnd - timeFirst;
    velocity = speedConst / diff;
    velocity_real = (velocity * 360) / 100;

    digitalWrite(ledPin, HIGH);
    Serial.print("The velocity is: ");
    Serial.println(velocity_real);
    Serial.print(" km/hr ");
    delay(500);
    digitalWrite(ledPin, LOW);
    delay(500);
  }
}

## 🖼️ Output Photo

## Speed Detection System

![Speed Detector](images/speed_detector.png)

