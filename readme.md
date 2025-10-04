# ULTRASONIC-BUZZER

## 📡 وصف المشروع

مشروع **ULTRASONIC-BUZZER** يستخدم حساس **الموجات فوق الصوتية (Ultrasonic Sensor - HC-SR04)** لاكتشاف المسافات، وعند اقتراب جسم إلى مسافة محددة، يتم تفعيل **جرس (Buzzer)** لإصدار صوت إنذار.

مثال عملي لأنظمة الإنذار أو مساعدة الوقوف في السيارات.

---

## 🧰 المتطلبات

- لوحة Arduino (مثل Uno أو Nano)
- حساس الموجات فوق الصوتية HC-SR04
- Buzzer (نشط أو غير نشط)
- مقاومة (في حالة Buzzer غير نشط)
- أسلاك توصيل
- برنامج Arduino IDE

---

## 🔌 التوصيل

### حساس HC-SR04:

| الطرف | إلى Arduino |
|-------|--------------|
| VCC   | 5V           |
| GND   | GND          |
| Trig  | D9           |
| Echo  | D8           |

### الجرس (Buzzer):

| الطرف | إلى Arduino |
|-------|-------------|
| +     | D7          |
| -     | GND         |

---

## 💻 كود Arduino

```cpp
const int trigPin = 9;
const int echoPin = 8;
const int buzzerPin = 7;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // إرسال نبضة
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // قراءة مدة رجوع النبضة
  long duration = pulseIn(echoPin, HIGH);
  // حساب المسافة بالسنتيمتر
  int distance = duration * 0.034 / 2;

  Serial.print("المسافة: ");
  Serial.print(distance);
  Serial.println(" سم");

  // تشغيل الجرس إذا كانت المسافة أقل من 20 سم
  if (distance < 20) {
    digitalWrite(buzzerPin, HIGH);
  } else {
    digitalWrite(buzzerPin, LOW);
  }

  delay(200);
}
