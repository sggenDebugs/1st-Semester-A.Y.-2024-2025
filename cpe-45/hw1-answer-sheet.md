1. In Arduino, loops happens when a block of code is executed over and over again and creates cycles called iterations. It can be controlled with certain conditions. For loops are frequently used to increment and decrement counters, or to initialize large numbers of pins at the same time. For loops evaluate a set of three parameters – the initialization value, the condition, and the iteration. For the while-loop, if the condition is true, the program will enter the body of the while loop and execute the body code in a loop for as long as the condition remains true. For the do-while loop, they work the same way as regular while loops, except that the body code is executed before the test for the condition occurs
2. The **if statement** is the most basic of all programming control structures. It allows you to make something happen or not, depending on whether a given condition is true. The **else statement** starts an event if the given condition is false. While, the **else if statement** can check a second condition if the first is false.
3. In order for the software to use trigonometric functions, the developer should put it contains the trigonometric function prototypes. The sine function calculates the sine of an angle, cosine function calculates the cosine of an angle, and the tangent calculates the tangent of an angle. The answer is always returned in radians.
4. I/O is done in Arduino in many methods. The pins on the Arduino board can be configured as either inputs or outputs using the pinMode function. After the pins are configured, the pins are processed using the digitalWrite, digitalRead and analogRead function.
5. Arduino sketches are actually written in C++ but a lot of the complexity has been abstracted so that you mainly will be responsible for two blocks of code: **setup and loop**. The setup code executes once at startup and is used to initialize the system. On the other hand, the loop continuously runs forever until it is interrupted.
6. _A sketch is the name that Arduino uses for a program_. It's the unit of code that is uploaded to and run on an Arduino board.
7. The Arduino Integrated Development Environment - or Arduino Software (IDE) - contains a text editor for writing code, a message area, a text console, a toolbar with buttons for common functions and a series of menus. It connects to the Arduino hardware to upload programs and communicate with them.
8. ![[Pasted image 20240922175734.png]]
```
9. 

void setup() {
	Serial.begin(9600); // 9600 is default baud rate for serial monitor
	while (!Serial) {
    ; // Wait for serial to connect
  }
  Serial.println("Trigonometric Function Example");
}

void loop(){
	double angleDegrees = 45.0;
	double angleRadians = radians(angleDegrees);

	float sineValue = sin(angleRadians);
	float cosineValue = cos(angleRadians);
    float tangentValue = tan(angleRadians);

	Serial.print("Angle (Degrees): ");
	Serial.println(angleDegrees);
	Serial.print("Sine: ");
	Serial.println(sineValue);
	Serial.print("Cosine: ");
	Serial.println(cosineValue);
	Serial.print("Tangent: ");
	Serial.println(tangentValue);
	
	delay(1000);
}
```

```
10. 
#include <Adafruit_LEDBackpack.h>

Adafruit_7segment display = Adafruit_7segment();

void setup() {
  // Initialize the 7-segment display
  display.begin(0x70);  // Default I2C address for Adafruit 7-segment display

  // Optional: start serial communication for debugging
  Serial.begin(9600);
}

void loop() {
  float angleDeg = 30;  // Angle in degrees

  // Convert angle from degrees to radians for trig functions
  float angleRad = radians(angleDeg);

  // Calculate sine, cosine, and tangent values
  float sineValue = sin(angleRad);
  float cosineValue = cos(angleRad);
  float tangentValue = tan(angleRad);

  // Convert the results to integers for display (scaled by 100 to show 2 decimal places)
  int sineInt = sineValue * 100;
  int cosineInt = cosineValue * 100;
  int tangentInt = tangentValue * 100;

  // Display Sine value
  displayValue(sineInt, "Sin");

  delay(2000);  // Wait for 2 seconds

  // Display Cosine value
  displayValue(cosineInt, "Cos");

  delay(2000);  // Wait for 2 seconds

  // Display Tangent value
  displayValue(tangentInt, "Tan");

  delay(2000);  // Wait for 2 seconds
}

// Function to display values on the 7-segment display
void displayValue(int value, String function) {
  // Clear the display
  display.clear();

  // Display the value on the serial monitor (for debugging)
  Serial.print(function);
  Serial.print(": ");
  Serial.println(value);

  // Handle negative values
  if (value < 0) {
    display.writeDigitRaw(0, 0x40); // Display negative sign on the first digit
    value = -value;
  }

  // Display the number with 4 digits, two of which will be decimal places
  display.print(value);  // Print integer
  display.writeDigitRaw(2, value % 100);  // Add decimal point
  display.drawColon(false);  // No colon needed for this display

  // Display the result on the 7-segment
  display.writeDisplay();
}
```