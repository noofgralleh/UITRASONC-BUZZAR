# UITRASONC-BUZZAR
#define trigPin 9
#define echoPin 10
#define buzzer 3

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // إرسال نبضة
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // استقبال الزمن
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2; // حساب المسافة بالس*
  }
