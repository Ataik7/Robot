### Robot
- Programming with Arduino
- Autonomous robot

### Code explanation


```
const int pinENA = 6;
const int pinIN1 = 7;
const int pinIN2 = 8;
const int pinIN3 = 9;
const int pinIN4 = 10;
const int pinENB = 11;
const int EchoPin = 4;
const int TriggerPin = 3;
const int sensorPin1 = 12;
const int sensorPin2 = 13;
const int waitTime = 250;
const int speed = 200;
const int pinMotorA[3] = { pinENA, pinIN1, pinIN2 };
const int pinMotorB[3] = { pinENB, pinIN3, pinIN4 };
```
There are several constants representing pin numbers, sensor configurations, and motor parameters.

<br>

```
void setup() {
  pinMode(TriggerPin, OUTPUT);
  pinMode(EchoPin, INPUT);
  pinMode(sensorPin1, INPUT);
  pinMode(sensorPin2, INPUT);
  pinMode(pinIN1, OUTPUT);
  pinMode(pinIN2, OUTPUT);
  pinMode(pinENA, OUTPUT);
  pinMode(pinIN3, OUTPUT);
  pinMode(pinIN4, OUTPUT);
  pinMode(pinENB, OUTPUT);
}
```
Here, the pin modes are configured for input and output.

<br>

```
void loop() {
  int cm = ping(TriggerPin, EchoPin);
  int value1 = digitalRead(sensorPin1);
  int value2 = digitalRead(sensorPin2);

  haciaDelante(pinMotorA, 200);
  haciaDelante(pinMotorB, 200);

  if (cm <= 15){
    haciaDelante(pinMotorA, 200);
    haciaDelante(pinMotorB, 200);
    delay(waitTime);
  }

  if (value1 == LOW) {
    haciaAtras(pinMotorA, 200);
    haciaDelante(pinMotorB, 200);
    delay(waitTime);
  }

  if (value2 == LOW) {
    haciaDelante(pinMotorA, 200);
    haciaAtras(pinMotorB, 200);
    delay(waitTime);
  }
}
```
- The ultrasonic sensor is used to measure distance (cm).
- If it detects an obstacle (cm <= 15), the robot stops briefly.
- If sensorPin1 is LOW, it moves backward.
- If sensorPin2 is LOW, it turns right.

<br>

```
void haciaAtras(const int pinMotor[3], int speed)

{

  digitalWrite(pinMotor[1], HIGH);

  digitalWrite(pinMotor[2], LOW);

  analogWrite(pinMotor[0], speed);

}


void haciaDelante(const int pinMotor[3], int speed)

{

  digitalWrite(pinMotor[1], LOW);

  digitalWrite(pinMotor[2], HIGH);

  analogWrite(pinMotor[0], speed);

}

void Parar(const int pinMotor[3])

{

  digitalWrite(pinMotor[1], LOW);

  digitalWrite(pinMotor[2], LOW);

  analogWrite(pinMotor[0], 0);

}
```
Here, the movement of the robot is controlled.

<br>

```
int ping(int TriggerPin, int EchoPin) {

  long duration, distanceCm;

  digitalWrite(TriggerPin, LOW);

  delayMicroseconds(4);

  digitalWrite(TriggerPin, HIGH);

  delayMicroseconds(10);

  digitalWrite(TriggerPin, LOW);

  duration = pulseIn(EchoPin, HIGH);

  distanceCm = duration * 10 / 292/ 2;

  return distanceCm;

}
```
The 'ping' function uses an ultrasonic sensor to measure distance in cm and returns the result with the 'return' statement.


