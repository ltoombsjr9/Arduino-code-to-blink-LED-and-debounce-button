# Arduino-code-to-blink-LED-and-debounce-button
Code necessary to make LED blink and to debounce button to make it work properly

#include <EasyButton.h>
#include <Adafruit_NeoPixel.h>

const int buttonPin = 7;
const int ledPin = 10;
const int numberOfPixels = 4;
const int delayVal = 500;

bool lastButtonState = LOW;

Adafruit_NeoPixel pixels(numberOfPixels, ledPin, NEO_GRB + NEO_KHZ800);

#define BAUDRATE 115200

EasyButton button(buttonPin);

void onPressed()
{
  Serial.println("Button pressed");
  
    lastButtonState = !lastButtonState;
    //digitalWrite(LED_BUILTIN, lastButtonState);

    if(lastButtonState == HIGH){
       pixels.clear(); 

  for(int i=0; i<numberOfPixels; i++) { 

    pixels.setPixelColor(i, pixels.Color(255, 0, 0));

    pixels.show();  

    delay(delayVal); 
    }
  } else {

    pixels.clear();
    pixels.show(); 

 }
}

void setup(){
  Serial.begin(BAUDRATE);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(LED_BUILTIN, OUTPUT);
  button.begin();
  button.onPressed(onPressed);
}

void loop(){
  button.read();
  
  }
