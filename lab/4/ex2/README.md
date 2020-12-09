

# Exercise 2
We have to upload the code from lab 3, build the circuit and see if its works
## Schematic 
![Test Image](https://github.com/LamJustine/2020-B-Bad-and-Boudji/blob/main/lab/4/ex2/130690584_703748360282401_3188846469530334827_n.jpg)

## Code
 ```Arduino
/*********************************************************************

  
*********************************************************************/

#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SH1106.h>

/* Puisque la bibliothèque est basée sur celle du SSD1306, le constructeur
prévoit qu'on passe le numéro de la broche RESET en argument. Mais le SH1106
n'a pas de broche RESET, alors on écrit n'importe quel entier (de préférence,
le numéro d'une broche de l'Arduino que vous n'utilisez pas). */
Adafruit_SH1106 display(23); 

/* Définition d'une image bitmap: logo du blog Électronique en Amateur
  Réalisée avec l'outil en ligne  http://javl.github.io/image2cpp/  */

const unsigned char myBitmap [] PROGMEM = {
// '130752316_4668778736528901_5167471492054194099_n', 128x64px

0xff, 0xff, 0xf0, 0x20, 0x60, 0x01, 0x00, 0x63, 0x03, 0x03, 0xf0, 0x3f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7b, 0x00, 0x00, 0x03, 0xc1, 0x80, 0x01, 0xf1, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7f, 0x00, 0x00, 0x07, 0xc3, 0x81, 0x21, 0xc1, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0xff, 0xc0, 0x00, 0x07, 0xe7, 0x00, 0x01, 0xe4, 0x7f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf2, 0x7f, 0x80, 0x00, 0x03, 0xc6, 0x00, 0x01, 0xff, 0x3f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0x7f, 0x80, 0x00, 0x01, 0xcc, 0x06, 0x01, 0xff, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7d, 0x30, 0x00, 0x03, 0xde, 0x07, 0x00, 0xff, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf8, 0x78, 0x33, 0x00, 0x00, 0xdc, 0x07, 0x80, 0x5f, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x78, 0x03, 0x00, 0x02, 0x00, 0x0f, 0x80, 0x7f, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7c, 0x00, 0x00, 0x1f, 0x20, 0x03, 0x81, 0xff, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7c, 0x00, 0x00, 0x03, 0xe0, 0x03, 0x01, 0xff, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7c, 0x00, 0x00, 0x00, 0xef, 0x80, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x7c, 0x00, 0x00, 0x00, 0x0f, 0x80, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x38, 0x00, 0x00, 0x00, 0x01, 0x80, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x20, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x60, 0x30, 0x00, 0x7f, 0xe7, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x30, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3e, 0x00, 0x3f, 0xfb, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf1, 0x70, 0x00, 0x00, 0x00, 0x00, 0x00, 0x7f, 0x80, 0x3f, 0xfc, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x60, 0x00, 0x00, 0x00, 0x00, 0x1c, 0x7f, 0xc0, 0x1f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x04, 0x00, 0x00, 0x00, 0x00, 0xb8, 0x7f, 0x80, 0x1f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x08, 0x00, 0x00, 0x00, 0x00, 0xf8, 0x1f, 0x00, 0x1f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xfc, 0x3c, 0x00, 0x00, 0x00, 0x00, 0x78, 0x0e, 0x00, 0x1f, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0xfc, 0x00, 0x00, 0x00, 0x00, 0x38, 0x06, 0x20, 0x18, 0xff, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0xfc, 0x30, 0x00, 0x03, 0x00, 0x00, 0x00, 0x18, 0x00, 0x7f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0xfc, 0x00, 0x00, 0x07, 0x00, 0x20, 0x00, 0x08, 0x00, 0x7f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x60, 0x80, 0x20, 0x00, 0x3f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xff, 0xc0, 0x00, 0x00, 0x00, 0x00, 0x40, 0xdb, 0xb8, 0x00, 0x3f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf7, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x40, 0xd3, 0xf8, 0x00, 0x1f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0xf8, 0x00, 0x01, 0xe0, 0x00, 0x40, 0x8f, 0xf8, 0x00, 0x1f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x98, 0x00, 0x01, 0x84, 0x00, 0x40, 0x07, 0xf0, 0x00, 0x0f, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0xde, 0x00, 0x07, 0x04, 0x80, 0x00, 0x00, 0xf0, 0x00, 0x03, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xfe, 0xfe, 0x00, 0x06, 0x01, 0x80, 0x00, 0x00, 0xf0, 0x00, 0x01, 0xff, 0xff, 0xff, 
0xff, 0xff, 0xfe, 0x1e, 0x00, 0x07, 0x71, 0x80, 0x00, 0x3f, 0xe0, 0x00, 0x00, 0x6f, 0xff, 0xff, 
0xff, 0xff, 0xfc, 0x00, 0x00, 0x03, 0x18, 0x00, 0x00, 0x3f, 0xc0, 0x00, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xfc, 0x40, 0x00, 0x03, 0x80, 0x00, 0x00, 0x1f, 0x00, 0x00, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xfd, 0xc0, 0x00, 0x03, 0x80, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf9, 0x80, 0x00, 0x03, 0xc0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3f, 0xff, 0xff, 
0xff, 0xff, 0xf1, 0x80, 0x06, 0x07, 0x60, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x7f, 0xff, 0xff, 
0xff, 0xff, 0xf9, 0x00, 0x0e, 0x07, 0x80, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x7e, 0x07, 0x80, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00, 0x3f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0xff, 0x07, 0x80, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00, 0x1f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x0f, 0x0f, 0x80, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x07, 0x02, 0x0f, 0x00, 0x00, 0x00, 0x00, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x03, 0x40, 0x0e, 0x00, 0x00, 0x00, 0x00, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x70, 0x06, 0x00, 0x00, 0x00, 0x00, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x78, 0x06, 0x00, 0x00, 0x00, 0x00, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x78, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x08, 0x10, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x10, 0x00, 0x00, 0x01, 0x00, 0x00, 0x20, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x03, 0x80, 0x00, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x20, 0x00, 0x00, 0x00, 0x03, 0x80, 0x80, 0x30, 0x00, 0x0f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x01, 0xf0, 0x00, 0x00, 0x00, 0x03, 0x80, 0x00, 0x70, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x01, 0xf0, 0x00, 0x00, 0x00, 0x03, 0x80, 0x00, 0xf8, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x03, 0xc0, 0x00, 0xf8, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x03, 0xc0, 0x03, 0xfc, 0x00, 0x8f, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x03, 0xc0, 0x03, 0xfc, 0x00, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x01, 0xe0, 0x07, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf4, 0x00, 0x00, 0x00, 0x00, 0x00, 0x01, 0xf0, 0x0f, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x01, 0xf8, 0x1f, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x01, 0xff, 0xff, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xfe, 0x01, 0xcf, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xfe, 0x01, 0xef, 0xff, 0xff, 
0xff, 0xff, 0xf0, 0x00, 0x00, 0x00, 0x00, 0x00, 0x20, 0xff, 0xff, 0xfc, 0x01, 0xef, 0xff, 0xff
  
};


void setup()   {

  display.begin();  // initialisation de l'afficheur
  display.clearDisplay();   // ça efface à la fois le buffer et l'écran
}


void loop() {



  /**************** Éxcriture de texte  ***************/

  // taille par défaut
  display.setCursor(30, 15);  // coordonnées du point de départ du texte
  display.setTextColor(WHITE);
  display.setTextSize(1);  // taille par défaut
  display.println("Team...");

  display.display();  // affichage à l'écran
  delay(1000);

  // deux fois plus gros
  display.setCursor(30, 35);  // coordonnées du point de départ du texte
  display.setTextSize(1.5);  // taille double
  display.println("BAD AND BOUDJI!");

  display.display();  // affichage à l'écran
  delay(1000);
  display.clearDisplay();  // on efface tout

  /******************** Dessiner une ligne ******************************************/

  // ligne horizontale au centre de l'écran
  display.drawLine(0, display.height() / 2, display.width() , display.height() / 2,  WHITE);

  // ligne verticale au centre de l'écran

  display.drawLine(display.width() / 2, 0, display.width() / 2, display.height(), WHITE);


  /********************* Dessiner des contours de formes géométriques ******************/

  display.drawRect( 15, 5, 30, 15, WHITE); // contour d'un rectangle
  display.drawCircle(95, 15, 8, WHITE);  // contour d'un cercle
  display.drawRoundRect(15, 40, 30, 16, 5, WHITE);  // contour d'un rectangle à coins arrondis
  display.drawTriangle(95, 40, 80, 55, 110, 55, WHITE);  // contour d'un triangle

  display.display();
  delay(1000);


  /******************* Dessiner des formes géométriqeus pleines *************************/

  display.fillRect( 15, 5, 30, 15, WHITE); // contour d'un rectangle
  display.fillCircle(95, 15, 8, WHITE);  // contour d'un cercle
  display.fillRoundRect(15, 40, 30, 16, 5, WHITE);  // contour d'un rectangle à coins arrondis
  display.fillTriangle(95, 40, 80, 55, 110, 55, WHITE);  // contour d'un triangle

  display.display();
  delay(1000);
  display.clearDisplay();
  
  /********************** Dessiner un pixel à la fois ***********************************************/


  // on trace une fonction sinusoidale, point par point
  for (int x = 1; x < 128; x++) {
    int y = 32 + round(16.0 * sin(x / 5.0));
    display.drawPixel(x, y, WHITE);
  }

  display.display();

  delay(1000);
  display.clearDisplay();


  /**************************** Dessiner une image  bitmap **********************************/

  // on affiche l'image stockée dans la constante myBitmap définie au début de ce fichier.

  display.fillRect(5,5,44,58,WHITE);  // fond blanc derrière l'image bitmap
  
  display.drawBitmap(0, 0, myBitmap, 64, 128, BLACK);



  display.display();
  delay(2000);
  display.clearDisplay();

}

```