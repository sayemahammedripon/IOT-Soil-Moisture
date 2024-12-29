# IOT-Soil-Moisture
We ran this code in arduiuno 
int sensor_pin = A0; // Sensor connected to analog pin A0
int white_light = 7; // White LED connected to digital pin 7
int red_light = 8;   // Red LED connected to digital pin 8

void setup()
{
  Serial.begin(9600);          // Start Serial communication
  pinMode(sensor_pin, INPUT);  // Set sensor pin as input
  pinMode(white_light, OUTPUT); // Set white LED pin as output
  pinMode(red_light, OUTPUT);   // Set red LED pin as output
}

void loop()
{
  int sensor_data = analogRead(sensor_pin); // Read moisture sensor data
  Serial.print("Sensor Data: ");
  Serial.println(sensor_data);

  if(sensor_data >= 0 && sensor_data <= 500)
  {
    // Turn on white LED for 0-500
    Serial.println("Moisture level low, White LED ON.");
    digitalWrite(white_light, HIGH); // Turn white LED on
    digitalWrite(red_light, LOW);    // Ensure red LED is off
  }
  else if(sensor_data >= 501 && sensor_data <= 700)
  {
    // No light for 501-700
    Serial.println("Moisture level medium, No LED.");
    digitalWrite(white_light, LOW); // Turn white LED off
    digitalWrite(red_light, LOW);   // Turn red LED off
  }
  else if(sensor_data >= 701)
  {
    // Turn on red LED for 701 and above
    Serial.println("Moisture level high, Red LED ON.");
    digitalWrite(white_light, LOW); // Ensure white LED is off
    digitalWrite(red_light, HIGH);  // Turn red LED on
  }
  else
  {
    // Default case: No LED
    Serial.println("Invalid sensor data.");
    digitalWrite(white_light, LOW);
    digitalWrite(red_light, LOW);
  }

  delay(100); // Short delay for stability
}
