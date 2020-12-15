# Second Steps
 **Description**:  This file shows how we continue our projet

We added the second sensor and plugged all the wires to see if the two sensors works both together :

![Branchement](https://github.com/efrei-paris-sud/2020-B-Bad-and-Boudji/blob/main/project/Step2/131570519_714866209166673_3110274308391363592_n.jpg)
![Screen](https://github.com/efrei-paris-sud/2020-B-Bad-and-Boudji/blob/main/project/Step2/131692346_178328550678658_3062877474122607788_n.png)

The sensor dectects the obstacle well and measures the distance between the two as you can see in the two pictures.

 ```Arduino
 
 /*
Mesure de distance à l'aide d'un capteur HC-SR04 et d'un Arduino
Projets DIY • Domotique  et Objets Connectés<iframe class="wp-embedded-content" sandbox="allow-scripts" security="restricted" style="position: absolute; clip: rect(1px, 1px, 1px, 1px);" title="« Projets DIY • Domotique  et Objets Connectés » &#8212; Domotique et objets connectés à faire soi-même" src="https://projetsdiy.fr/embed/#?secret=dl9kSPooob" data-secret="dl9kSPooob" width="600" height="338" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>

Circuit - repérage des broches
- VCC avec la broche 5V de l'Arduino
- GND avec la broche GND de l'Arduino
- Trig avec la broche 2 de l'Arduino
- Echo avec la broche 3 de l'Arduino

Librairie: HCSR04 by Martin Sosic


#include <HCSR04.h>

// defines pins numbers / definition des broches du capteur
const int trigPin = 2;
const int echoPin = 3;
 
// Initialize sensor that uses digital pins trigPin and echoPin / initialisation du capteur avec les broches utilisees.
UltraSonicDistanceSensor distanceSensor(trigPin, echoPin);
void setup() {
  // We initialize serial connection so that we could print values from sensor./ initialisation du port serie a 9600 band pour afficher les valeurs mesurees par le capteur.
  Serial.begin(9600); 
}
void loop() {
  // Every 500 miliseconds, do a measurement using the sensor and print the distance in centimeters./ toutes les 500 millisecondes nous faisons une mesure et nous affichons la distance en centimetre sur le port serie.
  Serial.println(distanceSensor.measureDistanceCm());
  delay(500);
}*/



#include <HCSR04.h>

// defines pins numbers / definition des broches du capteur
const int trigPin1 = 2;
const int echoPin1 = 3;
const int trigPinS = 4;
const int echoPinS = 5;
 
// Initialize sensor that uses digital pins trigPin and echoPin / initialisation du capteur avec les broches utilisees.
UltraSonicDistanceSensor distanceSensor1(trigPin1, echoPin1);
UltraSonicDistanceSensor distanceSensorS(trigPinS, echoPinS);


void setup() {
  // We initialize serial connection so that we could print values from sensor./ initialisation du port serie a 9600 band pour afficher les valeurs mesurees par le capteur.
  Serial.begin(9600); 
  int seuilPresence = 200;//distance entre sensor et sol
 
}
void loop() {
  // Every 200 miliseconds, do a measurement using the sensor and print the distance in centimeters./ toutes les 500 millisecondes nous faisons une mesure et nous affichons la distance en centimetre sur le port serie.
  
  Serial.println("sensor entrance distance ") ; Serial.println (distanceSensor1.measureDistanceCm());
  Serial.println("sensor out distance ") ; Serial.println(distanceSensorS.measureDistanceCm());
  delay(2000); // 200
}
 
 ```


