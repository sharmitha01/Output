**OUTPUT**
CODE
#define BLYNK_TEMPLATE_ID "TMPL3wpFP3MEc"
#define BLYNK_TEMPLATE_NAME "medicine reminder"
#define BLYNK_AUTH_TOKEN "zBneVJLkNr4pI6J3mKTwEQEGImWETtuP"

#define BLYNK_PRINT Serial
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

const int soundSensorPin = A0;
const int motionSensorPin = 2;

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "Redmi Note 10S";
char pass[] = "12345678";

BlynkTimer timer;
int soundFlag = 0;
int motionFlag = 0;

void sendSoundSensor() {
  int soundValue = analogRead(soundSensorPin);
  Serial.print("Sound sensor value: ");
  Serial.println(soundValue);

  int soundThreshold = 500;  // Adjust as needed

  if (soundValue > soundThreshold && soundFlag == 0) {
    Serial.println("Sound detected!");
    Blynk.logEvent("sound_alert", "Sound Detected");
    soundFlag = 1;
  } else if (soundValue <= soundThreshold) {
    Serial.println("No sound detected");
    soundFlag = 0;
  }
}

void sendMotionSensor() {
  int motionValue = digitalRead(motionSensorPin);

  if (motionValue == HIGH && motionFlag == 0) {
    Serial.println("Motion detected!");
    Blynk.logEvent("motion_alert", "Motion Detected");
    motionFlag = 1;
  } else if (motionValue == LOW) {
    Serial.println("No motion detected");
    motionFlag = 0;
  }
}

void setup() {
  pinMode(soundSensorPin, INPUT);
  pinMode(motionSensorPin, INPUT);

  Serial.begin(115200);
  Blynk.begin(auth, ssid, pass);

  timer.setInterval(5000L, sendSoundSensor);  // Adjust the interval as needed
  timer.setInterval(5000L, sendMotionSensor); // Adjust the interval as needed
}

void loop() {
  Blynk.run();a
  timer.run();
}



![WhatsApp Image 2023-11-23 at 10 21 27 PM (1)](https://github.com/sharmitha01/Output/assets/149594557/037f9cfe-9017-42d2-8b2c-91d8d4e52fa6)

![WhatsApp Image 2023-11-24 at 9 00 49 AM](https://github.com/sharmitha01/Output/assets/149594557/b4cd29aa-e021-473b-8622-9c3adabdadd0)

![WhatsApp Image 2023-11-23 at 9 40 19 PM](https://github.com/sharmitha01/Output/assets/149594557/9e966323-fc1f-435b-9056-97d28239ea07)

![WhatsApp Image 2023-11-23 at 10 21 27 PM (2)](https://github.com/sharmitha01/Output/assets/149594557/9e46b3ac-ffcf-4dfb-9d46-4c782a276f64)







https://github.com/sharmitha01/Output/assets/149594557/8d76fd78-2fee-4ede-a0a1-eedfa61ce40f





