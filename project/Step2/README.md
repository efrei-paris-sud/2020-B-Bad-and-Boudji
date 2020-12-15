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
 
 
 Then we added a counter for the number of persons who enter or exit :
 
 ```Arduino
 
 #define trigPin1 2 //dÃ©finition du 1er capteur on branche la borne trigger sur le pin 2 de la carte Arduino
#define echoPin1 3 //dÃ©finition du 1er capteur on branche la borne echo sur le pin 3 de la carte Arduino
#define trigPin2 4 //dÃ©finition du 2Ã¨me capteur on branche la borne trigger sur le pin 4 de la carte Arduino
#define echoPin2 5 //dÃ©finition du 2Ã¨me capteur on branche la borne echo sur le pin 5 de la carte Arduino

void setup() {
Serial.begin (9600); // on va utiliser notre ordinateur afin de lire ce que dit la carte Arduino
pinMode(trigPin1, OUTPUT); // on active la borne trigger du capteur 1
pinMode(echoPin1, INPUT); // on active la borne echo du capteur 1
pinMode(trigPin2, OUTPUT); // on active la borne trigger du capteur 2
pinMode(echoPin2, INPUT); // on active la borne echo du capteur 2
//Serial.println("Demarrage du programme"); // cette ligne est inutile c'est juste pour faire beau
}
unsigned int visitor = 0; // de base il y a personne dans notre magasin et visitor ne peut prendre une valeur negative
void loop() {
long duration1, distance1; // ici on dÃ©fini deux variables qui correspondent a la distance de l'obstacle
long duration2, distance2; // ici on dÃ©fini deux variables qui correspondent a la distance de l'obstacle
digitalWrite(trigPin1, HIGH);
delayMicroseconds(2); // test
digitalWrite(trigPin1, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin1, LOW);
delayMicroseconds(10); // test
digitalWrite(trigPin1, LOW);
duration1 = pulseIn(echoPin1, HIGH);
distance1 = duration1 / 58; // ici exprimee en cm cf : http://www.micropik.com/PDF/HCSR04.pdf
// Serial.print("Capteur 1: ");
// Serial.println(distance1); // si besoin pour deboguer
delay(500);

digitalWrite(trigPin2, HIGH);
delayMicroseconds(2); // test
digitalWrite(trigPin2, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin2, LOW);
delayMicroseconds(10); // test
digitalWrite(trigPin2, LOW);
duration2 = pulseIn(echoPin2, HIGH);
distance2 = duration2 / 58; // ici exprimee en cm cf : http://www.micropik.com/PDF/HCSR04.pdf
// Serial.print("Capteur 2: ");
// Serial.println(distance2); // si besoin pour deboguer
delay(500);

if(distance1 < 100 && distance2 > 100) { // si le capteur 1 rÃ©agit en premier
visitor = visitor + 1; // ALORS on ajoute +1 a la variable visitor
}
if(distance1 > 100 && distance2 < 100) { // si le capteur 2 rÃ©agit en second
visitor = visitor - 1; // ALORS on enleve 1 a la variable visitor
}
Serial.print("Nombre de personnes en magasin : "); // on s'en sert pour deboguer
Serial.println(visitor); // on s'en sert pour deboguer

}
 
 ```
We get this :

![Screen](https://github.com/efrei-paris-sud/2020-B-Bad-and-Boudji/blob/main/project/Step2/131889620_1314939608857401_9195753201624875662_n.png)

