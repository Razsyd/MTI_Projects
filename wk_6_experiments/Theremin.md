<img src="Theremin.jpg" width="350" style="horizontal-align:middle;margin:0px 50px">

           /* Quasi-theremin instrument

           Connect the photoresistor one leg to pin 0, and pin to +5V
           Connect a resistor (around 10k is a good value, higher
           values gives higher readings) from pin 0 to GND.

           ----------------------------------------------------

                      PhotoR     10K
            +5    o---/\/\/--.--/\/\/---o GND
                             |
            Pin 0 o-----------

           ----------------------------------------------------
           */

           int lightPin = A0;   //define a pin for Photo resistor
           //int ledPin = 16;     //define a pin for LED
           long brightness=0;
           int speakerPin = A5;
           int numTones = 10;
           int tones[] = {261, 277, 294, 311, 330, 349, 370, 392, 415, 440, 457};
           String notes[]={"mid C","C#","D","D#","E","E#","F","F#","G","G#","A"};

           int myTone = map (brightness, 0, 995, 0,10);

           void setup()
           {
               Serial.begin(9600);  //Begin serial communcation
               pinMode(speakerPin, OUTPUT);
           }
           void loop()
           {

              Serial.println(analogRead(lightPin));
           // Write the value of the photoresistor to the serial monitor.

             delay(100); //short delay for faster response to light.

              brightness = (analogRead(lightPin));
              myTone = map (brightness, 0, 995, 0,10);

              if (brightness > 50) {
                 tone(speakerPin, tones[myTone]);
                 Serial.println(myTone);
                 // Serial.println(notes[(int(brightness/90))]);
                 delay(10);
               }
             else noTone(speakerPin);
               Serial.println(brightness);            // Print to serial port
               delay(200);                          //pause for 200 millis
           }
