int ch1;

void setup() {
pinMode(2,OUTPUT); // 릴레이
pinMode(A1, OUTPUT); //모터핀 1
pinMode(A0, OUTPUT); // 모터핀 2
pinMode(10, OUTPUT); // GND
pinMode(5, INPUT); // 조이스틱
pinMode(13,OUTPUT); // 릴레이 출력
pinMode(7,INPUT_PULLUP); // 스위치 좌
pinMode(6,INPUT_PULLUP); // 스위치 우
Serial.begin(9600);
}

void loop() {

ch1 = pulseIn(5, HIGH, 25000);
Serial.print("Channel 1:"); // Print the value of
Serial.println(ch1); // each channel
Serial.println("");

if (digitalRead(7) == LOW && ch1<=1300)
{
  digitalWrite(10, LOW);
}
else if(digitalRead(6) == LOW && ch1>=1700)
{
  digitalWrite(10, LOW);
}
else if (ch1<=1300)
{
  digitalWrite(2,HIGH);
  digitalWrite(13,HIGH); 
  analogWrite(A1,1023);  
  analogWrite(A0,1023); 
  digitalWrite(10,HIGH);
  digitalWrite(7,HIGH);  
}
else if (ch1>=1700)
{
  digitalWrite(2,LOW); 
  digitalWrite(13,LOW); 
  analogWrite(A1, 1023);
  analogWrite(A0, 1023);
  digitalWrite(10, HIGH);
  digitalWrite(7,LOW);
}
else if (ch1>=1400 && ch1<=1650)
{
  digitalWrite(2,HIGH);
  analogWrite(A1,HIGH);
  analogWrite(A0,HIGH);
  digitalWrite(10,LOW);
  digitalWrite(7,HIGH);
  }
else
{
  digitalWrite(10, LOW); // 스위치 두개 잡으면 정방향,역방향 회전불가
}
}