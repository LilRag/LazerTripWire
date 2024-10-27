#include<Servo.h>
int intrud=0; //theres no intruder
int pr = 0; // photoresistor
int buzz = 13; // buzzer
int led = 4; // LED
int laser = 2; // Laser
int nointrud=0;
Servo myservo;


void setup(){
pinMode(pr, INPUT);
pinMode(buzz, OUTPUT);
pinMode(laser, OUTPUT);
pinMode(led, OUTPUT);
Serial.begin(9600);
myservo.attach(9,500,2500);
myservo.write(90);
}

void sound(){ // function to sound the alarm with a delay of 0.5 seconds
//tone(buzz, 700, 1000);
digitalWrite(buzz,HIGH); // turn on the alarm speaker
digitalWrite(led,HIGH); // turn on the alarm led
delay(1000);
digitalWrite(buzz,LOW); // turn off the alarm speaker
digitalWrite(led,LOW); // turn off the alarm led
delay(100);
}

void close_door()
{
for(int i=90;i>=0;i-=1)
{
myservo.write(i);
delay(10);
}
}

void open_door()
{
for(int i=0;i<=90;i+=1)
{
myservo.write(i);
delay(50);
}
}


void loop(){
int read = analogRead(pr);// read the sensor value from the photoresistor
Serial.println(read);// view / monitor the value of the sensor on the serial
digitalWrite(laser,HIGH); // turn on the lasers
float voltage = read * (5.0 / 1024.0);
Serial.print(voltage);
Serial.println(" Volt");
Serial.print("intruder present:");
Serial.println(intrud);
if (read<200)
{
nointrud=10;
sound();
if(intrud==0) //if intruder never tripped wire then run closing function
{
close_door(); //door closing function
intrud+=1;
delay(50);
}
}
else
{
nointrud-=1;
if(nointrud==0)
{
open_door();

}
intrud=0;
delay(500);
}

}
