# UART-Arduino-

#include <SoftwareSerial.h>

// Define RX and TX pins for SoftwareSerial (Router connection)
#define RX_PIN 10
#define TX_PIN 11

// Create a SoftwareSerial object for router communication
SoftwareSerial routerSerial(RX_PIN, TX_PIN);

void setup() {
  // Start communication with the router at 115200 baud
  routerSerial.begin(115200);

  // Start communication with the PC at 115200 baud
  Serial.begin(115200);

  // Prompt user
  Serial.println("Arduino is ready. Type commands to send to the router:");
}

void loop() {
  // Forward data from PC to router
  if (Serial.available()) {
    String command = Serial.readStringUntil('\n'); // Read input from PC
    routerSerial.println(command);                // Send to router
    Serial.println(command); // Confirm to PC
  }

  // Forward data from router to PC
  if (routerSerial.available()) {
    String response = routerSerial.readStringUntil('\n'); // Read from router
    Serial.println(response);       // Forward to PC
  }
}
