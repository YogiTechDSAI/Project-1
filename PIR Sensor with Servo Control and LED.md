#include <Servo.h>

int pirSensorPin = 2;   // PIR sensor connected to digital pin 2
int ledPin = 6;        // LED connected to digital pin 6
int servoPin = 9;       // Servo motor connected to digital pin 9

Servo servo;  // Creating a servo object

void setup() {
  pinMode(pirSensorPin, INPUT); //  PIR sensor pin as input
  pinMode(ledPin, OUTPUT);       //  LED pin as output
  servo.attach(servoPin);        // Attaching servo motor to pin
}

void loop() {
  int pirState = digitalRead(pirSensorPin); // Reading PIR sensor state

  if (pirState == HIGH) {
    digitalWrite(ledPin, HIGH);  // Turning on LED
    servo.write(90);             // servo moving to 90 degrees position
    delay(1000);                 // Delay for 1000 sec
  } else {
    digitalWrite(ledPin, LOW);   // Turn off LED
    servo.write(0);              // servo moving to 0 degrees position
  }
}
/*Here's how the code works:

The PIR sensor is connected to digital pin 2, the servo motor is connected to digital pin 9, and the LED is connected to digital pin 6.
Inside the setup() function, I set the appropriate pin modes, and attach the servo motor to its pin using the servo.attach() function.
In the loop() function, we continuously read the state of the PIR sensor using digitalRead().
If motion is detected (PIR sensor state is HIGH), the LED is turned on using digitalWrite() and the servo motor is moved to a 90-degree position using servo.write(90).
If no motion is detected (PIR sensor state is LOW), the LED is turned off using digitalWrite() and the servo motor is moved to a 0-degree position using servo.write(0).*/
