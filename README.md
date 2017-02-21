# Arduino-Accelerometer-step-count-
reading steps withing the arduino uno. Engineering 7B 
#include <math.h>
const int xpin = A3; 
const int ypin = A2; 
const int zpin = A1; 

float threshold = 136.5;

float xave = 512;
float yave = 512;
float zave = 512;


int steps,flag=0; 


void setup() { 
  Serial.begin(9600);
    Serial.println("Arduino is ready") ;
}

void loop() { 

  int acc=0;
  float totalvector[100]= {0}; 
  float totalaverage[100]={0};
    float xacc[100]={0};
    float yacc[100]={0}; 
    float zacc[100]={0};

for (int i=0; i<100 ; i++){
  
xacc[i] = float(analogRead(xpin));
delay(1);
yacc[i]= float(analogRead(ypin));
delay(1);
zacc[i] = float(analogRead(zpin)); 
delay(1);

totalvector[i] = sqrt(((xacc[i]-xave)*(xacc[i]-xave))+((yacc[i]-yave)*(yacc[i]-yave))+((zacc[i]-zave)*(zacc[i]-zave)));
totalaverage[i]= ((totalvector[i]+ totalvector[i-1])/2);
delay(1);

if (totalaverage[i]>threshold && flag==0){
  steps += 1;
  flag=1;
}
else if (totalaverage[i] < threshold && flag==1){
}
if (totalaverage[i]< threshold && flag==1)
{flag=0;}

Serial.println('\n');
Serial.print("steps=");
Serial.print(steps);
delay(100);
}
}
