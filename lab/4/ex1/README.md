

# Exercise 1 
We have to upload the led blink code from lab 1, build the circuit and see if its works
## Schematic 
![Test Image](https://github.com/LamJustine/2020-B-Bad-and-Boudji/blob/main/lab/4/ex1/130448685_302881177654537_63442097216143856_n.jpg)

## Code
 ```Arduino
 
const int led = 12;
 
// the setup routine runs once when you press reset:
void setup() {                
  // initialize the digital pin as an output.
  pinMode(led, OUTPUT);     
}
 
// the loop routine runs over and over again forever:
void loop() {
  digitalWrite(led, HIGH);      // turn the LED on (HIGH is the voltage level)
  delay(1000);                  // wait for a second
  digitalWrite(led, LOW);       // turn the LED off by making the voltage LOW
  delay(1000);                  // wait for a second
}

```
