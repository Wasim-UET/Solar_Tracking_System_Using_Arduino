#include <Servo.h>

Servo horizontal; // Create servo object to control the horizontal axis
int servoPin = 9; // Digital pin connected to the servo motor

// LDR sensor pins
int ldrLeft = A0;  // Left LDR pin
int ldrRight = A1; // Right LDR pin

int initialPosition = 90; // Starting position of the servo (degrees)
int tolerance = 30;       // Sensitivity tolerance to prevent jitter

void setup() {
  horizontal.attach(servoPin);
  horizontal.write(initialPosition); // Move servo to starting position
  Serial.begin(9600);
}

void loop() {
  // Read analog values from both LDRs
  int leftValue = analogRead(ldrLeft);
  int rightValue = analogRead(ldrRight);
  
  // Print values to Serial Monitor for debugging
  Serial.print("Left: ");
  Serial.print(leftValue);
  Serial.print(" | Right: ");
  Serial.println(rightValue);
  
  // Calculate the difference between the two LDR readings
  int diff = abs(leftValue - rightValue);
  
  // Check if the difference exceeds the tolerance threshold
  if (diff > tolerance) {
    int currentAngle = horizontal.read();
    
    if (leftValue > rightValue) {
      // Light is stronger on the left; move servo left (increase angle)
      if (currentAngle < 180) {
        horizontal.write(currentAngle + 1);
      }
    } else {
      // Light is stronger on the right; move servo right (decrease angle)
      if (currentAngle > 0) {
        horizontal.write(currentAngle - 1);
      }
    }
  }
  
  // Short delay to allow the servo to reach position smoothly
  delay(20);
}
