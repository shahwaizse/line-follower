int motorPin1 = 5; // INT1 of L298N mini
int motorPin2 = 6; // INT2 of L298N mini
int motorPin3 = 9; // INT3 of L298N mini
int motorPin4 = 10; // INT4 of L298N mini

int leftSensor = 2;
int middleSensor = 3;
int rightSensor = 4;
int extraSensor1 = 7;
int extraSensor2 = 8;

int foundPath = 0;

int sensorsArray[5] = {2, 3, 4, 7, 8};

void setup() {
  pinMode(leftSensor, INPUT);
  pinMode(rightSensor, INPUT);
  pinMode(motorPin1, OUTPUT);
  pinMode(motorPin2, OUTPUT);
  pinMode(motorPin3, OUTPUT);
  pinMode(motorPin4, OUTPUT);
  delay(1000);
  Serial.begin(9600);
}

void loop() {
  // if (digitalRead(leftSensor) == LOW && digitalRead(rightSensor) == LOW && digitalRead(middleSensor) == LOW) {
  //   // moveMotor(3);
  //   while(digitalRead(leftSensor) == HIGH || digitalRead(rightSensor) == HIGH || digitalRead(middleSensor) == HIGH) {
  //     moveMotor(1);
  //   }
  // }
  if (digitalRead(leftSensor) == LOW && digitalRead(rightSensor) == LOW) {
    moveMotor(2);
  }

  if (digitalRead(leftSensor) == HIGH && digitalRead(rightSensor) == HIGH) {
    moveMotor(2);
  }

  if(digitalRead(leftSensor) == LOW && digitalRead(rightSensor) == HIGH) {
    moveMotor(3);
    delay(50);
  }

  if(digitalRead(leftSensor) == HIGH && digitalRead(rightSensor) == LOW) {
    moveMotor(1);
    delay(50);
  }

  if(digitalRead(leftSensor) == HIGH && digitalRead(rightSensor) == HIGH) {
    moveMotor(2);
    delay(50);
  }

  if (digitalRead(leftSensor) == LOW && digitalRead(rightSensor) == LOW && digitalRead(middleSensor) == LOW && digitalRead(extraSensor1) == LOW && digitalRead(extraSensor2) == LOW) {
    // while(digitalRead(leftSensor) == LOW || digitalRead(rightSensor) != HIGH || digitalRead(middleSensor) != HIGH) {
    //   moveMotor(1);
    //   delay(50);
    // }
    while(1) {
      moveMotor(1);
      for(int i = 0; i < 5; i++) {
        if(digitalRead(sensorsArray[i]) == HIGH) {
          foundPath = 1;
          break;
        }
      }
      if(foundPath == 1){
        foundPath = 0;
        break;
      }
    }
  }
}

int speed = 190; //from 0-255

void moveMotor(int direction) {
  switch (direction) {
    case 1: // right
      analogWrite(motorPin1, speed);
      analogWrite(motorPin2, 0);
      analogWrite(motorPin3, speed);
      analogWrite(motorPin4, 0);
      break;
    case 2: // forward
      analogWrite(motorPin1, speed);
      analogWrite(motorPin2, 0);
      analogWrite(motorPin3, 0);
      analogWrite(motorPin4, speed);
      break;
    case 3: // left
      analogWrite(motorPin1, 0);
      analogWrite(motorPin2, speed);
      analogWrite(motorPin3, 0);
      analogWrite(motorPin4, speed);
      break;
    case 4: // stop
      analogWrite(motorPin1, 0);
      analogWrite(motorPin2, 0);
      analogWrite(motorPin3, 0);
      analogWrite(motorPin4, 0);
      break;
  }
}

// void moveMotorOld(int direction) {
//   switch (direction) {
//     case 1: // Turn right (reversed)
//       digitalWrite(motorPin1, HIGH);
//       digitalWrite(motorPin2, LOW);
//       digitalWrite(motorPin3, HIGH);
//       digitalWrite(motorPin4, LOW);
//       break;
//     case 2: // Turn left (reversed)
//       digitalWrite(motorPin1, LOW);
//       digitalWrite(motorPin2, HIGH);
//       digitalWrite(motorPin3, LOW);
//       digitalWrite(motorPin4, HIGH);
//       break;
//     case 3: // Move forward
//       digitalWrite(motorPin1, HIGH);
//       digitalWrite(motorPin2, LOW);
//       digitalWrite(motorPin3, LOW);
//       digitalWrite(motorPin4, HIGH);
//       break;
//     case 4: // Stop
//       digitalWrite(motorPin1, LOW);
//       digitalWrite(motorPin2, LOW);
//       digitalWrite(motorPin3, LOW);
//       digitalWrite(motorPin4, LOW);
//       break;
//   }
// }
