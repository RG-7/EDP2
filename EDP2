const int trigpin=13, echopin=12, Pin=4;
long duration=0;
int cm, l, r, flag = 0, d = 0;
static int c = 0;
unsigned long x = millis();
long interval = 500;
 
void setup()
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  Serial.begin(9600);
}
 
void loop()
{
  if (Serial.read() == 'e' || flag == 1) flag = 1;
  if (flag == 1) run_buggy();
}
 
void run_buggy()
{
    if (digitalRead(Pin) == HIGH) {
      d = pulseIn(Pin, HIGH);
 
      if (d > 1700 && d < 1900) {
        Serial.println("Ping 2: Gantry 1");
        Serial.print("Ping 2: d = "); Serial.println(d);
        stop_buggy(); delay(1000);
      }
 
      if (d > 2700 && d < 2900) {
        Serial.println("Ping 2: Gantry 2");
        Serial.print("Ping 2: d = "); Serial.println(d);
        stop_buggy(); delay(1000);
      }
 
      if (d > 700 && d < 900) {
        Serial.println("Ping 2: Gantry 3");
        Serial.print("Ping 2: d = "); Serial.println(d);  
        stop_buggy(); delay(1000);
      }
    }
 
    l = digitalRead(A0);
    r = digitalRead(A1);
    if (l == 1 && r == 1) forward();
    if (l == 0 && r == 1) left();
    if (l == 1 && r == 0) right();
    if (l == 0 && r == 0) {
      unsigned long y = millis();
      if ((y - x) > interval) {
        c++;
        x = millis();
      }

      Serial.print("Ping 2: count = "); Serial.println(c);
 
      if (c == 2) { //park exit
        right();
        delay(150); //adjust
      }
 
      else if (c == 5) {  //Park entry
        right();
        delay(200); //adjust
      }
 
      else if (c == 6) { //park
        forward(); delay(1200);
        stop_buggy();
        Serial.println("Ping 2: COMPLETED!");
        flag = 0;
      }
 
      else forward();
    }

      ultrasonic();
     
}

void ultrasonic(){
  delay(50);
  digitalWrite(trigpin, LOW);
  delayMicroseconds(50);
  digitalWrite(trigpin, HIGH);
  digitalWrite(echopin, HIGH);
  cm=(duration/0.027);
  Serial.print("Ping 2: Distance: "); Serial.print(cm); Serial.println(" cm");
  if (cm < 20) {stop_buggy(); delay(1000);
  }
}


void stop_buggy()  
{
  digitalWrite(5, LOW);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);
  digitalWrite(8, LOW);
}
 
void forward()
{
  digitalWrite(5, HIGH);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);
  digitalWrite(8, HIGH);
}
 
void left()
{
  digitalWrite(5, HIGH);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);
  digitalWrite(8, LOW);
}
 
void right()
{
  digitalWrite(5, LOW);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);
  digitalWrite(8, HIGH);
}
