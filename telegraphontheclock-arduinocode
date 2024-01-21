#include <Keypad.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

const int buzzerPin = 10;
const int redPin = 11;
const int greenPin = 12;
const int bluePin = 13;

LiquidCrystal_I2C lcd(0x27, 16, 2);

const byte ROWS = 4;
const byte COLS = 4;
char keys[ROWS][COLS] = {
  {'1', '2', '3'},
  {'4', '5', '6'},
  {'7', '8', '9'},
  {'*', '0', '#'}
};
byte rowPins[ROWS] = {9, 8, 7, 6};
byte colPins[COLS] = {5, 4, 3, 2};
Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

const int numPatterns[10][5] = {
  {2, 2, 2, 2, 2},
  {1, 2, 2, 2, 2},
  {1, 1, 2, 2, 2},
  {1, 1, 1, 2, 2},
  {1, 1, 1, 1, 2},
  {1, 1, 1, 1, 1},
  {2, 1, 1, 1, 1},
  {2, 2, 1, 1, 1},
  {2, 2, 2, 1, 1},
  {2, 2, 2, 2, 1}
};

int currentNumber = 0;
int score = 0;
int lives = 3;
bool readyToPlay = false;
bool playAgain = false;

void setup() {
  pinMode(buzzerPin, OUTPUT);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  lcd.begin();
  lcd.setCursor(0, 0);
  lcd.print("Are you ready?");
  lcd.setCursor(0, 1);
  lcd.print("Press # to start!");
  lightRGB(0, 0, 255);  // Set initial light color to blue
}

void loop() {
  if (!readyToPlay) {
    char keyPressed = waitForKey();
    if (keyPressed == '#') {
      readyToPlay = true;
      lcd.clear();
      lcd.print("Score: 0");
      lcd.setCursor(0, 1);
      lcd.print("Lives: 3");
    }
  } else {
    playNumberPattern();
    char keyPressed = waitForKey();

    if (keyPressed == '#') {
      playAgain = true;
    } else if (keyPressed == (currentNumber + '0')) {
      score++;
      displayScore();
      playCorrectSound();
      lightRGB(0, 255, 0);  // Green
      delay(2000);  // Delay for 2 seconds
      lightRGB(0, 0, 255);  // Blue
    } else {
      lives--;
      displayLives();
      if (lives == 0) {
        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("Bomb Has");
        lcd.setCursor(0, 1);
        lcd.print("Exploded!");
        playExplosionSound();
        lightRGB(255, 0, 0);  // Red
        delay(1500);  // Delay for 1.5 seconds
        lcd.clear();
        lcd.print("Score: ");
        lcd.print(score);
        lcd.setCursor(0, 1);
        lcd.print("Play again? #");
        lightRGB(255, 255, 0);  // Yellow
        while (true) {
          char keyPressed = waitForKey();
          if (keyPressed == '#') {
            score = 0;
            lives = 3;
            readyToPlay = false;
            playAgain = false;
            lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Are you ready?");
            lcd.setCursor(0, 1);
            lcd.print("Press # to start!");
            lightRGB(0, 0, 255);  // Blue
            break;
          }
        }
      } else {
        playErrorSound();
        lightRGB(255, 0, 0);  // Red
        delay(2000);  // Delay for 2 seconds
        lightRGB(0, 0, 255);  // Blue
      }
    }
  }

  if (playAgain) {
    resetGame();
  }

  delay(1000);
}

void resetGame() {
  lcd.clear();
  lcd.print("Play again? #");
  lightRGB(255, 255, 0);  // Yellow

  while (true) {
    char keyPressed = waitForKey();
    if (keyPressed == '#') {
      score = 0;
      lives = 3;
      readyToPlay = false;
      playAgain = false;
      lcd.clear();
      lcd.print("Are you ready?");
      lcd.setCursor(0, 1);
      lcd.print("Press # to start!");
      lightRGB(0, 0, 255);  // Blue
      break;
    }
  }
}

void playNumberPattern() {
  currentNumber = random(0, 10);
  int* pattern = numPatterns[currentNumber];

  for (int i = 0; i < 5; i++) {
    if (pattern[i] == 1) {
      digitalWrite(buzzerPin, HIGH);
      delay(350);
      digitalWrite(buzzerPin, LOW);
    } else {
      digitalWrite(buzzerPin, HIGH);
      delay(850);
      digitalWrite(buzzerPin, LOW);
    }
    delay(200);
  }
}

char waitForKey() {
  char keyPressed = NO_KEY;
  while (keyPressed == NO_KEY) {
    keyPressed = keypad.getKey();
  }
  return keyPressed;
}

void displayScore() {
  lcd.setCursor(7, 0);
  lcd.print(score);
}

void displayLives() {
  lcd.setCursor(7, 1);
  lcd.print(lives);
}

void playCorrectSound() {
  tone(buzzerPin, 1000, 500);
  delay(500);
  noTone(buzzerPin);
}

void playErrorSound() {
  tone(buzzerPin, 2000, 200);
  delay(200);
  noTone(buzzerPin);
}

void playExplosionSound() {
  lightRGB(255, 0, 0);
  for (int i = 0; i < 3; i++) {
    tone(buzzerPin, 500, 1000);
    delay(1000);
  }
  noTone(buzzerPin);
}

void lightRGB(int red, int green, int blue) {
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}
