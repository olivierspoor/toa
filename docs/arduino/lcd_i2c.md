# LiquidCrystal met I2C

I2C (*Inter-Integrated Circuit*) is een methode voor seriële datacommunicatie met een breed scala aan toepassingen. Het is mogelijk om een LCD-scherm via een speciale I2C-adapter aan te sluiten op een Arduino. Het grote voordeel hiervan is dat er minder kabels nodig zijn. 

![i2c-adapter](../assets/images/I2C.jpg)

Deze adapter heeft slechts vier aansluitingen: 

* GND - Grond wordt verbonden aan de GND van de Arduino.
* VCC - Voltage wordt verbonden met de 5 Volt pin op de Arduino.
* SDA - *Serial Data Line* 
* SCL - *Serial Clock Line*

Zie de blauwe pijl op de afbeelding hieronder voor de SDA en SCL ingangen op de Arduino.

![Arduino-SDA_SCL](../assets/images/SDA_SCL.png)

Er zitten 16 pinnen aan het LCD-scherm en 16 pinnen aan de I2C-adapter. De volgorde is hier belangrijk. Er staan echter weinig herkennigstekens op de adapter. Kijk dus goed naar de afbeelding hieronder om te zien hoe de twee op het breadboard aangesloten moeten worden.

![LCD-I2C](../assets/images/LCD_I2C.jpg)

## Bibliotheek

Om gebruik te kunnen maken van het scherm via de I2C-adapter is een Library (Bibliotheek) nodig. Dit is *niet* dezelfde als degene die al reeds is geïnstalleerd in Arduino IDE en zal dus nog toegevoegd moeten worden. Dit kan op de volgende manier:

**Bibliotheken beheren:** Druk op CTRL + Shift + I.

Of via het menu: 

*Hulpmiddelen > Bibliotheken beheren...*

Hier kun je zoeken naar `LiquidCrystal_I2C`. Als je dan een beetje naar beneden scrollt zie je de [volgende bibliotheek](https://arduino.cc/reference/en/libraries/liquidcrystal-i2c/). 

![Library](../assets/images/Library_I2C.png)

Klik vervolgens op installeren. Hierna is de bibliotheek geïnstalleerd en klaar om gebruikt te worden.

## De code

Wanneer je een (nieuwe) bibliotheek gebruikt om iets aan te sturen met een Arduino, is het noodzakelijk om de juiste code erbij te zoeken. Deze is meestal te vinden op de [site](https://arduino.cc/reference/en/libraries/liquidcrystal-i2c/) van arduino zelf of anders op de [site](https://github.comjohnrickman/LiquidCrystal_I2C) van de beheerder van de bibliotheek.


## Hello World!

De code hieronder laat "Hello World!" op het scherm zien en telt vervolgens de seconden sinds dat de code is geupload. 


```arduino
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,20,4);

void setup(){
  lcd.init();

  lcd.backlight();
  lcd.setCursor(0,0);
  lcd.print("Hello World!");
}

void loop(){
  lcd.setCursor(0,1);
  lcd.print(millis() / 1000);
}
```

Voor het oproepen van een bibliotheek in een schets wordt `#include` gebruikt. Vervolgens staat de naam van de bibliotheek tussen `< >`. 
Een andere manier om een bibliotheek toe te voegen is door deze te kiezen vanuit het menu:

*Schets > Bibliotheek gebruiken > ...*

Nieuwe geïnstalleerde bibliotheken staan meestal onderaan. 

In bovenstaand voorbeeld worden twee bibliotheken gebruikt:

* `<Wire.h>` - Dit is een bibliotheek voor I2C communicatie.
* `<LiquidCrystal_I2C.h>` - Dit is de nieuwe geïnstalleerde bibliotheek wat interactie met het LCD-scherm mogelijk maakt.

Vervolgens stellen het scherm in met `LiquidCrystal_I2C lcd(0x27,20,4)` waarbij `0x27` het (standaard)adres is voor deze seriële communicatie. `20,4` geeft het aantal karakters per regel aan: 4 regels, 20 karakters per regel. 

`lcd.init()` maakt het scherm klaar voor gebruik.

`lcd.backlight()` zet de achtergrondverlichting aan.

`lcd.setCursor([kolom],[rij])` zet de cursor op een specifieke plek. Linksboven is in dit geval positie `0,0`. Rechtsonder is `19,3`.

Vervolgens kan er geprint worden met `lcd.print()`. Als dit gaat om tekst (datatype: `str`) dan moet dit tussen aanhalingstekent `" "` staan.

Dit alles staat in de `void setup()` omdat dit alles slechts een keer wordt uitgevoerd. In de `void loop()` wordt de tijd sinds het uploaden bijgehouden in seconden. Hiervoor wordt `millis()` (tijd in milliseconden) gebruikt. Deze wordt op de eerste positie van de tweede regel geprint. 


## Contrast 
Het kan zijn dat het scherm moeilijk leesbaar is doordat het te licht of te donker is. Dit kan bijgesteld worden door middel van een potmeter. Dit is het blauwe gedeelte op de I2C (zie foto bovenaan). Om dit bij te stellen kan er gebruik gemaakt worden van een kleine schroevendraaier.  



Om het scherm leeg te maken wordt `lcd.clear()` gebruikt.

```arduino
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,20,4);

void setup(){
  lcd.init();
  lcd.clear();
}

void loop(){

}
```
