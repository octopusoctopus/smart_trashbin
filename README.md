# smart_trashbin
거리가 15cm미만이 되면 문이 열리고 5초 뒤에 닫히는 




```cpp
#include<Servo.h>

#define trig D3
#define echo D2
Servo servo_door;
float distance ;
void setup() {
  Serial.begin(9600);
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  // put your setup code here, to run once:
  servo_door.attach(D4);

  servo_door.write(20);
}

void loop() {
  // put your main code here, to run repeatedly:
measureDistance();

  if (distance <15 ) {
  doorOpen();
  delay(5000);
  doorClose();
  
}
  

  delay(500);
}

void measureDistance(){
  
  digitalWrite(trig, LOW);
  digitalWrite(echo, LOW);
  delayMicroseconds(2);
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
 
  unsigned long duration = pulseIn(echo, HIGH);
 
  distance = duration / 29.0 / 2.0;

  Serial.print(distance);
  Serial.println("cm");
 

}
void doorOpen(){
  servo_door.write(100);
  servo_door.attach(D4);
  delay(20);
  
}

void doorClose(){
  servo_door.write(20);
  delay(200);
  servo_door.detach();


}
```
