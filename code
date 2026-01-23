#define trigPin 8
#define echoPin 7
#define Rled 2
#define Yled 3
#define Gled 4
#define buzzer 10
#define photocell A0
#define autoLight 6
void setup() {
Serial.begin(9600);

Serial.println("Home Security System");
Serial.println("Name: Jurell "); //replace with your name

pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(Rled, OUTPUT);
pinMode(Yled, OUTPUT);
pinMode(Gled, OUTPUT);
pinMode(buzzer, OUTPUT);
pinMode(autoLight, OUTPUT);
}
void loop() {
//=== Automated Light ===
//read from the light sensor to determine the lighting condition
int value=analogRead(photocell);
//uncomment the line below, open the serial plotter to see the effect on the light
//Serial.println(value);
if (value > 450) {
digitalWrite(autoLight, HIGH);
Serial.println("The automated light is ON");
}
else {
digitalWrite(autoLight, LOW);
}
//==== Distance Sensor ===
long duration, distance, inches;
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
// Read the echo signal
//Read duration for roundtrip distance
duration = pulseIn(echoPin, HIGH);
//Convert duration to distance in units of inches
distance = (duration /2) * 0.0135 ;
if (distance <= 12) { //Outer IF statement units of inches
if (distance <=6){ //Alert range condition
Serial.println("Alert! Possible Intruder.");
digitalWrite(Rled, HIGH); //Alert green LED on
digitalWrite(Yled, LOW);
digitalWrite(Gled, LOW);
}
if (distance <12 and distance > 6){ //Warning range condition
digitalWrite(Rled, LOW);
digitalWrite(Yled, HIGH); //Warning yellow LED on
digitalWrite(Gled, LOW);
}
//==================== Beeping Rate Code Start ======
tone(buzzer,500);
for (int i= distance; i>0; i--)
delay(10);
noTone(buzzer);
for (int i= distance; i>0; i--)
delay(10);
//==================== Beeping Rate Code End =======
}
else{ //Safe range condition
digitalWrite(Rled, LOW);
digitalWrite(Yled, LOW);
digitalWrite(Gled, HIGH); //Safe distance green LED on
noTone(buzzer);
}//end of outer IF statement
delay(100); //pause program to stabilize sensor readings
} //end of loop
