/* ECHOPOD - ESP32 Ultrasonic & Vibration Motors device coded by Daksh and Deepak
Devloped by chitvansh and harshita
*/
#define FRONT_TRIG 5
#define FRONT_ECHO 18
#define LEFT_TRIG 17  
#define LEFT_ECHO 19
#define RIGHT_TRIG 16
#define RIGHT_ECHO 21

#define FRONT_MOTOR 25
#define LEFT_MOTOR 26
#define RIGHT_MOTOR 27

// ranges defination
#define WARNING_MIN 50   // cm
#define WARNING_MAX 120  // cm  

void setup() {
  Serial.begin(115200);
  
  // Ultrasonic definations given here
  pinMode(FRONT_TRIG, OUTPUT); pinMode(FRONT_ECHO, INPUT);
  pinMode(LEFT_TRIG, OUTPUT);  pinMode(LEFT_ECHO, INPUT);
  pinMode(RIGHT_TRIG, OUTPUT); pinMode(RIGHT_ECHO, INPUT);
  
  // Motor definations given here 
  pinMode(FRONT_MOTOR, OUTPUT);
  pinMode(LEFT_MOTOR, OUTPUT); 
  pinMode(RIGHT_MOTOR, OUTPUT);
  
  // In begnining motors OFF
  digitalWrite(FRONT_MOTOR, LOW);
  digitalWrite(LEFT_MOTOR, LOW);
  digitalWrite(RIGHT_MOTOR, LOW);
  
  Serial.println("Echopod Ready - Motors only (No Buzzer)");
}

void loop() {
  // Reading of sensor mentioned earlier is taking place here
  int frontDist = getDistance(FRONT_TRIG, FRONT_ECHO);
  int leftDist  = getDistance(LEFT_TRIG, LEFT_ECHO);
  int rightDist = getDistance(RIGHT_TRIG, RIGHT_ECHO);
  
  // the controling commands of moters are here 
  controlMotorVibration(FRONT_MOTOR, frontDist, WARNING_MIN, WARNING_MAX);
  controlMotorVibration(LEFT_MOTOR,  leftDist,  WARNING_MIN, WARNING_MAX);
  controlMotorVibration(RIGHT_MOTOR, rightDist, WARNING_MIN, WARNING_MAX);
  
  // waring are to be given in the below command
  printWarning("FRONT", frontDist);
  printWarning("LEFT",  leftDist);
  printWarning("RIGHT", rightDist);
  
  delay(100); // Main loop timing
}

// distance given by sensors are being used here in "cm" unit
int getDistance(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  long duration = pulseIn(echoPin, HIGH, 30000); // timeout added
  if (duration == 0) return -1; // No echo
  
  int distance = duration * 0.034 / 2;
  return distance;
}

// Motor vibration and dist are given here
void controlMotorVibration(int motorPin, int distance, int minDist, int maxDist) {
  if (distance >= maxDist || distance < 0) {
    digitalWrite(motorPin, LOW); // No warning
    return;
  }
  
  if (distance <= minDist) {
    digitalWrite(motorPin, HIGH); // Continuous vibration
    return;
  }
  
  // here it is the delay time
  int delayTime = map(distance, minDist, maxDist, 50, 1000);
  
  digitalWrite(motorPin, HIGH);
  delay(delayTime);
  digitalWrite(motorPin, LOW);
}


void printWarning(String direction, int distance) {
  if (distance >= WARNING_MIN && distance <= WARNING_MAX && distance > 0) {
    Serial.print(direction);
    Serial.print(" WARNING: ");
    Serial.print(distance);
    Serial.println(" cm");
  }
}
