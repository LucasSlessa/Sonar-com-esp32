#include <ESP32Servo.h>
#include <Ultrasonic.h>

const int triggerPin = 14;
const int echoPin = 12;
Ultrasonic ultrasonic(triggerPin, echoPin); // Instância do sensor de ultrassom

Servo servo; //instância do servo

// pinos para os sensores infravermelhos
const int rightIRPin = 27;
const int leftIRPin = 26;

// Defina os pinos para os motores DC
const int motor1A = 4;
const int motor1B = 5;
const int motor2A = 18;
const int motor2B = 19;

const int servoPin = 23; // Pino para o servo

void forward() {
  // Implemente a lógica para mover para frente usando os motores DC
  digitalWrite(motor1A, HIGH);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, HIGH);
  digitalWrite(motor2B, LOW);
}

void turnLeft() {
  // Implemente a lógica para virar para a esquerda usando os motores DC
  digitalWrite(motor1A, LOW);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, HIGH);
  digitalWrite(motor2B, LOW);
}

void turnRight() {
  // Implemente a lógica para virar para a direita usando os motores DC
  digitalWrite(motor1A, HIGH);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, LOW);
  digitalWrite(motor2B, LOW);
}

void stop() {
  // Implemente a lógica para parar o robô
  digitalWrite(motor1A, LOW);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, LOW);
  digitalWrite(motor2B, LOW);
}

void setup() {
  Serial.begin(115200);

  // Inicialize os pinos dos sensores infravermelhos como entradas
  pinMode(rightIRPin, INPUT);
  pinMode(leftIRPin, INPUT);

  // Inicialize os pinos dos motores DC como saídas
  pinMode(motor1A, OUTPUT);
  pinMode(motor1B, OUTPUT);
  pinMode(motor2A, OUTPUT);
  pinMode(motor2B, OUTPUT);

  // Inicialize o pino do servo
  servo.attach(servoPin);
}

void loop() {
  // Leitura do sensor de ultrassom
  int distance = ultrasonic.read();

  // Controle do servo
  if (distance > 1 && distance < 15) {
    // Defina a posição do servo para 90 graus (para frente)
    servo.write(90);
  } else {
    // Defina a posição do servo para 0 graus (para parar ou ajustar a direção conforme necessário)
    servo.write(0);
  }

  // Leitura dos sensores infravermelhos
  int rightIRValue = digitalRead(rightIRPin);
  int leftIRValue = digitalRead(leftIRPin);

  // Controle de movimento dos motores DC
  if (rightIRValue == LOW && leftIRValue == HIGH) {
    // Vire para a esquerda
    turnLeft();
  } else if (rightIRValue == HIGH && leftIRValue == LOW) {
    // Vire para a direita
    turnRight();
  } else if (rightIRValue == LOW && leftIRValue == LOW) {
    // Se ambos os sensores estiverem lendo baixo, pode ser necessário fazer um ajuste no seu código para evitar situações indesejadas
  } else {
    // Mova para frente
    forward();
  }
}
