
int sensor = 3;
int led = 2;
int ldr ;
unsigned long t=0;
const int hot = 87;
const int cold = 75;
void setup()
{
Serial.begin(9600);
pinMode(sensor, INPUT);
pinMode(ldr, INPUT);
pinMode(led, OUTPUT);
pinMode(A5, INPUT);
pinMode(10, OUTPUT);
pinMode(9, OUTPUT);
digitalWrite(led,LOW);
}
void loop()
{
int sensor1 = analogRead(A5);
float voltage = (sensor1 / 1024.0) * 5.0;
float tempC = (voltage - .5) * 100;
float tempF = (tempC * 1.8) + 32;
Serial.print("temp: ");
Serial.print(tempF);
if (tempF < cold) { //cold
digitalWrite(10, HIGH);
digitalWrite(9, LOW);
Serial.println("Cold.");
}
else if (tempF >= hot) { //hot, ikaw yun!
digitalWrite(10, LOW);
digitalWrite(9, HIGH);
Serial.println("Hot.");
}
ldr = analogRead(0);
Serial.println(ldr);
if(digitalRead(sensor)== HIGH && ldr<800)
{
t = millis();
digitalWrite(led,HIGH); }
else {
if( millis() > t+5000){
digitalWrite(led,LOW);
} }
delay(1000);
}
