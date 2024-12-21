# IR SENSOR INFO
/* This is code of Ir sensor interfaced with arduino. this code contains the library of IRsensor of arduino ide. 
For this code we are using the sensor named TSOP1838 IR sensor. the code also work with other sensor.
the circuit diagram for the code is 
sensor         -->  arduino I/O ;
pin1(signal)   -->     pin6 ;
pin2(gnd)      -->     gnd ;
pin3(Vcc)      -->      5V ;
*/

// # IR SENSOR CODE
#include <IRremote.h>

IRrecv recv(6);
bool state1 = false;
bool state2 = false;
bool state3 = false;
bool state4 = false;
bool state5 = false;
void setup() {
  // put your setup code here, to run once:
recv.enableIRIn();
Serial.begin(9600);
pinMode(2,OUTPUT);
pinMode(3,OUTPUT);
pinMode(4,OUTPUT);
pinMode(5,OUTPUT);
pinMode(7,OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
if(recv.decode()){
//  Serial.println(recv.decodedIRData.decodedRawData,HEX);
// above line use to detect the hex code of remote button 

  if(recv.decodedIRData.decodedRawData == 0xF20DFF00){
    Serial.println("led 1");
    state1 = !state1;
    toggle(2,state1);
    //digitalWrite(2,HIGH);
  }
  if(recv.decodedIRData.decodedRawData == 0xE619FF00){
    Serial.println("led 2");
    state2 = !state2;
    toggle(3,state2);
    //digitalWrite(3,HIGH);
  }
  if(recv.decodedIRData.decodedRawData == 0xE41BFF00){
    Serial.println("led 3");
    state3 = !state3;
    //digitalWrite(4,HIGH);
    toggle(4,state3);
  }
  if(recv.decodedIRData.decodedRawData == 0xFE01FF00){
    Serial.println("led 4");
    state4 = !state4;
    //digitalWrite(5,HIGH);
    toggle(5,state4);
  }
  if(recv.decodedIRData.decodedRawData == 0xEE11FF00){
    Serial.println("all off");
    digitalWrite(2,LOW);
    digitalWrite(3,LOW);
    digitalWrite(5,LOW);
    digitalWrite(4,LOW);
  }
delay(100);
recv.resume();
} 
}

void toggle(int x,bool y)
{
  if(y==true)
  digitalWrite(x,HIGH);
  else
  digitalWrite(x,LOW);
}

