# Een nieuw karakter maken

Je kunt met de LiquidCrystal bibliotheek een eigen karakter maken. Dit beslaat één vakje op het display. Hieronder zie je een voorbeeld van hoe je dit doet.

## Code

```c
#include <LiquidCrystal_PCF8574.h>
#include <Wire.h>

LiquidCrystal_PCF8574 lcd(0x27);

byte smiley[8] ={
    B00000,
    B01010,
    B01010,
    B00000,
    B10001,
    B10001,
    B01110,
    B00000};


void setup() {
  lcd.begin(20,4);  
  lcd.setBacklight(255);  
  lcd.createChar(1,smiley); 
  
  lcd.setCursor(10,1);
  lcd.write(1);
}

void loop() {
  
}
```

Een aantal regels heb je als het goed is eerder gezien. Een aantal regels zijn nieuw. Laten we de code stap voor stap bekijken. 

```c
// Allereerst roepen we de nodige bibliotheken op.
#include <LiquidCrystal_PCF8574.h>  
#include <Wire.h>

// We verbinden het LCD-scherm met de bibliotheek en geven het de naam `lcd`.
LiquidCrystal_PCF8574 lcd(0x27); 

```
Vervolgens gebeurt er iets nieuws. Dit lijkt ingewikkeld, maar wat je ervan moet begrijpen is eenvoudig.

```c
byte smiley[8] ={
    B00000,
    B01010,
    B01010,
    B00000,
    B10001,
    B10001,
    B01110,
    B00000};
```
Het begint met een datatype (*byte*) en variabele naam (*smiley*). Daarna wordt feitelijk het karakter pixel voor pixel weergegeven. Deze bestaat uit 8 regels van 5 pixels.
Een `1` zet de pixel aan en een `0` is uit. Hieronder zie je links hoe een karakter-vakje is ingedeeld, en rechts hoe de smiley eruit komt de zien.

![smiley](/docs/assets/lcd/smiley.png)

Dit is echter nog niet genoeg om de smiley daadwerkelijk op het scherm te plaatsen. 

De bibliotheek beschikt over een aantal posities om een teken in op te slaan. Voor het gemak gaan we uit van positie 1 t/m 8. 
`lcd.createChar(1, smiley)` is de regel die jouw tekentje beschikbaar maakt om te printen. Deze regel koppelt de informatie van `smiley` aan , in dit geval, positie 1. 
  
Voordat je iets naar het scherm print, wil je altijd aangegeven _waar_ je iets wilt printen. Dit doe je met `lcd.setCursor(kolom,rij)`. 

Vervolgens kun je je tekentje printen met `lcd.write(1)`. De `1` verwijst hier naar de `1` uit `lcd.createChar(1, smiley)` en die verwijst naar `byte smiley[8]` bovenaan je code. 