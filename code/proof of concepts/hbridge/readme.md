# H-Bridge proof of concept

minimale hard- & software + stappenplan dat aantoont dat 2 motoren onafhankelijk van elkaar kunnen draaien, en (traploos) regelbaar zijn in snelheid en draairichting.

<img width="472" height="631" alt="image" src="https://github.com/user-attachments/assets/85799242-c4ea-4838-b2ac-27f41ebb17c3" />









// === TB6612FNG PoC: 2 motoren onafhankelijk, traploos fwd/rev ===
// Pinout zoals jij aangaf + PWMA/PWMB toegevoegd
//
// Motor A: AIN1=6, AIN2=5, PWMA=3
// Motor B: BIN1=9, BIN2=10, PWMB=11
// STBY pin: naar 5V (of zet op OUTPUT HIGH als je een pin gebruikt)

#define AIN1 6
#define AIN2 5
#define PWMA 3   // PWM voor motor A

#define BIN1 9
#define BIN2 10
#define PWMB 11  // PWM voor motor B

void setup() {
  pinMode(AIN1, OUTPUT);
  pinMode(AIN2, OUTPUT);
  pinMode(PWMA, OUTPUT);

  pinMode(BIN1, OUTPUT);
  pinMode(BIN2, OUTPUT);
  pinMode(PWMB, OUTPUT);

  Serial.begin(9600);
  Serial.println(F("TB6612FNG PoC klaar. Commando's: a=+NNN/-NNN, b=+NNN/-NNN"));
}

// Motorsturing met signed speed [-255..255]
void motorA(int spd) {
  spd = constrain(spd, -255, 255);
  if (spd >= 0) {
    digitalWrite(AIN1, HIGH);
    digitalWrite(AIN2, LOW);
    analogWrite(PWMA, spd);
  } else {
    digitalWrite(AIN1, LOW);
    digitalWrite(AIN2, HIGH);
    analogWrite(PWMA, -spd);
  }
}

void motorB(int spd) {
  spd = constrain(spd, -255, 255);
  if (spd >= 0) {
    digitalWrite(BIN1, HIGH);
    digitalWrite(BIN2, LOW);
    analogWrite(PWMB, spd);
  } else {
    digitalWrite(BIN1, LOW);
    digitalWrite(BIN2, HIGH);
    analogWrite(PWMB, -spd);
  }
}

void loop() {
  // Demo: ramp Motor A vooruit, dan achteruit
  for (int s=0; s<=255; s+=20) { motorA(s); delay(100); }
  for (int s=255; s>=0; s-=20) { motorA(s); delay(100); }
  for (int s=0; s<=255; s+=20) { motorA(-s); delay(100); }
  for (int s=255; s>=0; s-=20) { motorA(-s); delay(100); }

  // Zelfde voor Motor B
  for (int s=0; s<=255; s+=20) { motorB(s); delay(100); }
  for (int s=255; s>=0; s-=20) { motorB(s); delay(100); }
  for (int s=0; s<=255; s+=20) { motorB(-s); delay(100); }
  for (int s=255; s>=0; s-=20) { motorB(-s); delay(100); }

  // Tegelijk onafhankelijk
  motorA(200);
  motorB(-150);
  delay(1500);
  motorA(0);
  motorB(0);
  delay(1000);
}


