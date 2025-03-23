const int leds[] = {2, 3, 4, 5};
const int buttons[] = {9, 8, 7, 6};
const int buzzer = 10;
int sequence[100];
int level = 1;

void setup() {
  Serial.begin(9600);
  for (int i = 0; i < 4; i++) {
    pinMode(leds[i], OUTPUT);
    pinMode(buttons[i], INPUT_PULLUP);
  }
  pinMode(buzzer, OUTPUT);
  randomSeed(analogRead(0));
  for (int i = 0; i < 100; i++) {
    sequence[i] = random(0, 4);
  }
  openingAnimation();
}

void openingAnimation() {
  int melody[] = {262, 294, 330, 349};
  for (int i = 0; i < 4; i++) {
    digitalWrite(leds[i], HIGH);
    tone(buzzer, melody[i], 200);
    delay(200);
    digitalWrite(leds[i], LOW);
    delay(50);
  }
  for (int i = 3; i >= 0; i--) {
    digitalWrite(leds[i], HIGH);
    tone(buzzer, melody[i], 200);
    delay(200);
    digitalWrite(leds[i], LOW);
    delay(50);
  }
  noTone(buzzer);
}

void lightUp(int led) {
  digitalWrite(leds[led], HIGH);
  tone(buzzer, 1000);
  delay(300);
  digitalWrite(leds[led], LOW);
  noTone(buzzer);
  delay(100);
}

void successTone() {
  tone(buzzer, 1500);
  delay(300);
  noTone(buzzer);
}

void failureTone() {
  for (int i = 0; i < 3; i++) {
    tone(buzzer, 500);
    delay(100);
    noTone(buzzer);
    delay(100);
  }
}

void showSequence() {
  for (int i = 0; i < level; i++) {
    lightUp(sequence[i]);
    delay(300);
  }
}

bool checkPlayerInput() {
  for (int i = 0; i < level; i++) {
    bool pressed = false;
    while (!pressed) {
      for (int j = 0; j < 4; j++) {
        if (digitalRead(buttons[j]) == LOW) {
          lightUp(j);
          if (j != sequence[i]) {
            failureTone();
            return false;
          }
          pressed = true;
        }
      }
    }
  }
  successTone();
  return true;
}

void loop() {
  showSequence();
  if (checkPlayerInput()) {
    level++;
    delay(500);
  } else {
    Serial.println(" Wrong! Try Again !.");
    level = 1;
    delay(1000);
  }
}
