# Proof of Concepts

Een proof of concept is een combinatie van minimale hard- en software om eenvoudig aan te tonen dat iets werkt.  
Proof of concepts kunnen enerzijds als eerste poging dienen om een bepaald onderdeel van het project werkend te krijgen. Anderzijds kunnen ze tijdens het debuggen van het finale project dienen als test om eventuele hardware problemen te elimineren bij onduidelijke problemen.
<br />  
<br />
Een proof of concept bestaat uit
* een elektronisch schema (indien van toepassing)
* minimale code om de voorop gestelde zaken te demonstreren
* minimale uitleg / aandachtspunten
<br />
De elektronische schakelingen van de proof of concepts komen bij voorkeur overeen met deze van de uiteindelijke linefollower, zodat de code zonder aanpassingen op het finale project kan draaien.

// Pin definities voor Arduino naar L293D
int motor1Pin1 = 4;  // Verbonden met pin 2 van de L293D (motor 1)
int motor1Pin2 = 5;  // Verbonden met pin 7 van de L293D (motor 1)
int motor2Pin1 = 6;  // Verbonden met pin 10 van de L293D (motor 2)
int motor2Pin2 = 7;  // Verbonden met pin 15 van de L293D (motor 2)
int enable1Pin = 9;  // Verbonden met pin 1 van de L293D (Enable motor 1)
int enable2Pin = 10; // Verbonden met pin 9 van de L293D (Enable motor 2)

// Sensor pinnen
int sensorLeft = A0;  // Linker sensor
int sensorRight = A1; // Rechter sensor

void setup() {
  // Stel motorpinnen en enable pinnen in als uitgang
  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);
  pinMode(enable1Pin, OUTPUT);
  pinMode(enable2Pin, OUTPUT);

  // Stel sensorpinnen in als ingang
  pinMode(sensorLeft, INPUT);
  pinMode(sensorRight, INPUT);

  // Enable motoren
  digitalWrite(enable1Pin, HIGH);
  digitalWrite(enable2Pin, HIGH);
}

void loop() {
  int leftState = digitalRead(sensorLeft);
  int rightState = digitalRead(sensorRight);

  if (leftState == LOW && rightState == LOW) {
    // Beide sensoren detecteren de lijn, ga vooruit
    motorForward();
  } else if (leftState == HIGH && rightState == LOW) {
    // Linker sensor is van de lijn af, stuur naar links
    turnLeft();
  } else if (leftState == LOW && rightState == HIGH) {
    // Rechter sensor is van de lijn af, stuur naar rechts
    turnRight();
  } else {
    // Geen lijn gedetecteerd, stop de motoren
    stopMotors();
  }
}

void motorForward() {
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
}

void turnLeft() {
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, HIGH);
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
}

void turnRight() {
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, HIGH);
}

void stopMotors() {
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, LOW);
}
