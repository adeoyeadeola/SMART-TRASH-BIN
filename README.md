# SMART-TRASH-BIN


An **Arduino-based Smart Trash Bin** that uses an ultrasonic sensor and servo motor to automatically open the lid when someone comes near. This project helps promote **contactless waste disposal** and is great for **smart homes, schools, and public spaces**. 
 Overview  
This system detects motion/objects near the trash bin using an **ultrasonic sensor**.  
When an object (like a hand) comes within a set distance, a **servo motor** opens the lid automatically. After a few seconds, the lid closes again.

⚙️ Components Used  
- Arduino Uno
- Ultrasonic Sensor (HC-SR04)  
- Servo Motor (SG90
- Breadboard and jumper wires  
- Power supply

- Code
- // Smart Trash Bin with Ultrasonic Sensor + Servo
#include <Servo.h>

Servo servoMotor;  

int trigPin = 9;   // Ultrasonic Sensor TRIG pin
int echoPin = 10;  // Ultrasonic Sensor ECHO pin
int servoPin = 3;  // Servo Motor pin

long duration;
int distance;

void setup() {
  servoMotor.attach(servoPin);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  servoMotor.write(0);  // Lid closed
  Serial.begin(9600);
}

void loop() {
  // Send ultrasonic pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read echo time
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2; // Convert to cm

  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance < 20) {  
    servoMotor.write(90);   // Open lid
    delay(3000);            // Wait 3 seconds
    servoMotor.write(0);    // Close lid
  }
}
