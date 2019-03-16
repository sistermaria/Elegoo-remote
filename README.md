# Elegoo-remote
Elegoo remote control

key	Hex code	Decimal code
power	FFFFFFFF	
0	FF6897	167384455
1	FF30CF	16724175
2	FF18E7	16718055
3	FF7A85	16743045
4	FF10EF	16716015
5	FF38C7	16726215
6	FF5AA5	16734885
7	FF42BD	16728765
8	FF4AB5	16730805
9	FF52AD	16732845
Up symbol	FF906F	16748865
Down symbol	FFE02FD	16712445
Vol+	FF629D	16736925
Func stop	FFE21D	16769565
Arrow to right 2 bars	FF02FD	16712445
2 arrows line left	FF22DD	16720605
2 arrows line right	FFC23D	16761405
		


Remote dig11(Arduino)
sketch feb09d(basic) ;remote with LED dig13
sketch feb09e ;remote with 3 LEDs

REMOTE ELEGOO



#include <IRremote.h>
 
int IR_Recv = 11;   //IR Receiver Pin 11
int bluePin = 10;
int greenPin = 9;
int yellowPin = 8;
 
IRrecv irrecv(IR_Recv);
decode_results results;
 
void setup(){
  Serial.begin(9600);  //starts serial communication
  irrecv.enableIRIn(); // Starts the receiver
  pinMode(bluePin, OUTPUT);      // sets the digital pin as output
  pinMode(greenPin, OUTPUT);      // sets the digital pin as output
  pinMode(yellowPin, OUTPUT);      // sets the digital pin as output 

}
 
void loop(){
  //decodes the infrared input
  if (irrecv.decode(&results)){
    long int decCode = results.value;
    Serial.println(results.value);
    //switch case to use the selected remote control button
    switch (results.value){
      case 16738455: //when you press the 0 button
        digitalWrite(bluePin, HIGH);
        break;   
      
       case 16724175: //when you press the 1 button
        digitalWrite(greenPin, HIGH);
        break;           
     
       case 16718055: //when you press the 2 button
        digitalWrite(yellowPin, HIGH);
        break;
      
      case 16743045: //when you press the 3 button
        digitalWrite(bluePin,LOW);
        break;
      
      case 16716015: //when you press the 4 button
        digitalWrite(greenPin,LOW);
      break;
      
      case 16726215: //when you press the 5 button
        digitalWrite(yellowPin,LOW);
      break;
      
      
    }
    irrecv.resume(); // Receives the next value from the button you press
  }
  delay(10);
}

