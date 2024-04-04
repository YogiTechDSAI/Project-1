#include <Servo.h>

int trigPin = 10; // Pin connected to the trigger pin on the ultrasonic sensor
int echoPin = 13; // Pin connected to the echo pin on the ultrasonic sensor
int servoPin1 = 11; // Pin connected to servo motor 1
int servoPin2 = 12; // Pin connected to servo motor 2

Servo servo1;
Servo servo2;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  
  servo1.attach(servoPin1);
  servo2.attach(servoPin2);

  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = (duration / 2) / 29.1; // Convert the time into distance (cm)

  if (distance < 50) { // Adjusted this value based on my setup
    // If object detected within 50cm, rotate servo motors
    servo1.write(180); // Rotate servo1 to 180 degrees
    servo2.write(180); // Rotate servo2 to 180 degrees
    delay(100); // Delay
  } else {
    // If no object detected, stop servo motors
    servo1.write(0); // Stop servo1
    servo2.write(0); // Stop servo2
  }

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  if(distance < 50)
  {
    Serial.println("UV Detected");
  }
  else{
    Serial.println("UV notDetected");
  }
  delay(500);
}
/*

The code triggers an ultrasonic sensor to emit UV waves and detect it with servo motor. 
If an object is within a certain limited distance, it rotates a servo motor by 180 degrees. The detection status is printed to the serial monitor.
This loop continues indefinitely, allowing the system to detect objects with ultrasonic waves and adjust the position of the servo motor accordingly.*/
