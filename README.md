#include <SoftwareSerial.h>

// Define the software serial pins for communication with Voice Recognition Module
SoftwareSerial voiceSerial(2, 3); // RX, TX pins (adjust as necessary)

// Pin for controlling an LED (or other device)
const int ledPin = 13;

void setup() {
  // Start serial communication for debugging
  Serial.begin(9600);
  voiceSerial.begin(9600);

  pinMode(ledPin, OUTPUT); // Initialize LED pin as output

  // Wait for the Voice Recognition Module to be ready
  Serial.println("Initializing Voice Recognition Module...");
  delay(2000);

  // Load the voice model (stored in the Voice Recognition Module V3)
  // The model is assumed to be pre-trained with commands like "Turn on light" and "Turn off light"
  if (voiceSerial.available()) {
    Serial.println("Voice recognition module is ready.");
  } else {
    Serial.println("Failed to communicate with the Voice Recognition Module.");
  }
}

void loop() {
  // Check if voice command data is available
  if (voiceSerial.available()) {
    int command = voiceSerial.read(); // Read the recognized command from the voice module
    
    // Print the recognized command
    Serial.print("Command received: ");
    Serial.println(command);

    // Process the command (here we use command numbers as placeholders)
    // Example: 0 for "Turn on light", 1 for "Turn off light"
    if (command == 0) {
      digitalWrite(ledPin, HIGH); // Turn on the LED
      Serial.println("Turn on light command received.");
    }
    else if (command == 1) {
      digitalWrite(ledPin, LOW);  // Turn off the LED
      Serial.println("Turn off light command received.");
    }
    else {
      Serial.println("Unrecognized command.");
    }
  }

  delay(100); // Small delay for stability
}
