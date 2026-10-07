# mini-project

#define GAS_SENSOR_PIN    D6  // GPIO12
#define SOUND_SENSOR_PIN  D7  // GPIO13
#define IR_SENSOR_PIN     D2  // GPIO4
#define LED_PIN           D5  // GPIO14
#define BUZZER_PIN        D1  // GPIO5

void setup() {
  pinMode(GAS_SENSOR_PIN, INPUT);
  pinMode(SOUND_SENSOR_PIN, INPUT);
  pinMode(IR_SENSOR_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(LED_PIN, LOW);
  digitalWrite(BUZZER_PIN, LOW);

  Serial.begin(9600);
  Serial.println("Gas, Sound & IR Monitoring Started");
}

void loop() {
  int gasState = digitalRead(GAS_SENSOR_PIN);
  int soundState = digitalRead(SOUND_SENSOR_PIN);
  int irState = digitalRead(IR_SENSOR_PIN);

  bool alert = false;

  // Gas detected
  if (gasState == LOW) {
    Serial.println("⚠️ GAS DETECTED!");
    alert = true;
  }

  // Object detected
  if (irState == LOW) {
    Serial.println("🚷 IR OBJECT DETECTED!");
    alert = true;
  }

  if (alert) {
    digitalWrite(LED_PIN, HIGH);
    digitalWrite(BUZZER_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
    digitalWrite(BUZZER_PIN, LOW);
    Serial.println("Environment Normal");
  }

  Serial.println("--------------------");
  delay(500);
}
