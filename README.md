# blind_man

This device can be used by the blind man. It detect obstacles wherever he move.
It can be embedd in the cap of the blind person.
Whenever any obstacle is encountered buzer start beeps.

Arduino Code

<pre>
<code>
#define trigPin 12 //trigger pin of Ultrasonic Sensor
#define echoPin 13 //echo pin of Ultrasonic Sensor

void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(7, OUTPUT); //Pin for Red Led
  pinMode(6, OUTPUT); //Pin for Green Led
}

void loop() {
  // put your main code here, to run repeatedly:
 int duration,distance;
 digitalWrite(trigPin,HIGH);
 delayMicroseconds(1000);
 digitalWrite(trigPin,LOW);
 duration=pulseIn(echoPin,HIGH); //Record for how much time echoPin is high
 distance=(duration/2)/29.1; //Calculate distance

 if(distance>=200 || distance<=0){
  Serial.println("Out of range");
 }
 else if(distance>=0 && distance<=30){
  beepFast(); //Call beepFast function
  Serial.print(distance);
  Serial.println("cm");
 }
 else if(distance>=31 && distance<=50){
  Serial.print(distance);
  Serial.println("cm");
  beepMedium(); //Call beepMedium function
 }
 else{
  beepNo(); //Call beepNo function
  Serial.print(distance);
  Serial.println("cm");
 }
}

void beepFast(){
  tone(8,440,200); //At pin 8 Buzzer play a tone for 200 miliseconds at the frquency of 440 
  digitalWrite(7,HIGH); //Turn on Red Led
  delay(50);
  noTone(8); //Turn off buzzer tone
  digitalWrite(7,LOW); //Turn off Red Led
  delay(300);
}

void beepMedium(){
  tone(8,440,200); //At pin 8 Buzzer play a tone for 200 miliseconds at the frquency of 440
  digitalWrite(7, HIGH); //Turn on Red Led
  delay(200);
  noTone(8); //Turn off buzzer tone
  digitalWrite(7,LOW); //Turn off Red Led
  delay(300);
}

void beepNo(){
  noTone(8); //Turn off buzzer tone
  digitalWrite(6,HIGH); //Turn on Green Led
  delay(300);
  digitalWrite(6,LOW);//Turn off Green Led
}
</code>
</pre>

<p>Schematic for the Blind Man Device</p>

<img src = "https://github.com/abhisheksharma1310/blind_man/blob/main/Blind%20Man%20Device%20Schematic.png">


