#include "SevSeg.h"
SevSeg sevseg; 
unsigned long previousMillis = 0;
const long interval = 1000;
int seconds = 0;
int minutes = 0;
int count = 0;
int button = 0;
int buzzer = 1;
int timerRunning = false;
int lastButtonState = HIGH;

void setup(){
  byte numDigits = 4;
  byte digitPins[] = {10, 11, 12, 13};
  byte segmentPins[] = {9, 2, 3, 5, 6, 8, 7, 4};

  pinMode(button, INPUT_PULLUP);  
  pinMode(buzzer, OUTPUT);

  bool resistorsOnSegments = true; 
  bool updateWithDelaysIn = true;
  byte hardwareConfig = COMMON_CATHODE; 
  sevseg.begin(hardwareConfig, numDigits, digitPins, segmentPins, resistorsOnSegments);
}

void loop() {
int currentButtonState = digitalRead(button);

if (timerRunning == false) {

if (currentButtonState != lastButtonState) {
  if (currentButtonState == LOW) {
      minutes = 25;
      timerRunning = true; 
    }
  }
  delay(50); 
}
  lastButtonState = currentButtonState;

if (timerRunning == true) {
  timer(); 
}

 }

void timer() {
   unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    
    seconds = seconds - 1;

    if (seconds < 0) {
      seconds = 59;
      minutes = minutes - 1;
      
      if (minutes < 0) {
        minutes = 0;
        seconds = 0;
        count = count + 1;
          digitalWrite(buzzer, HIGH); 
          delay(1000);                  
          digitalWrite(buzzer, LOW);
        timerRunning = false;

          if (count % 2 == 0) { 
            minutes = 25;
            timerRunning = true;
            timer();
          } else {
            minutes = 5;
            timerRunning = true;
            timer();
          }
      }
    }
}
    int displayTime = (minutes * 100) + seconds;
    sevseg.setNumber(displayTime, 2); 
    sevseg.refreshDisplay(); 
}
