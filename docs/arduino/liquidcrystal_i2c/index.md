# LiquidCrystal met I2C

I2C (*Inter-Integrated Circuit*) is een methode voor seriële datacommunicatie met een breed scala aan toepassingen. Het is mogelijk om een LCD-scherm via een speciale I2C-adapter aan te sluiten op een Arduino. Het grote voordeel hiervan is dat er minder kabels nodig zijn. 

![I2C](/docs/assets/lcd/i2c.jpg)

## Aansluiten

Deze adapter heeft slechts vier aansluitingen: 

* GND - Grond wordt verbonden aan de GND van de Arduino.
* VCC - Voltage wordt verbonden met de 5 Volt pin op de Arduino.
* SDA - *Serial Data Line* 
* SCL - *Serial Clock Line*

Zie de blauwe pijl op de afbeelding hieronder voor de SDA en SCL ingangen op de Arduino.

![SDA_SCL](/docs/assets/lcd/sda_scl.png)

Er zitten 16 pinnen aan het LCD-scherm en 16 pinnen aan de I2C-adapter. De volgorde is hier belangrijk. Er staan echter weinig herkennigstekens op de adapter. Kijk dus goed naar de afbeelding hieronder om te zien hoe de twee op het breadboard aangesloten moeten worden.

![LCD_I2C](/docs/assets/lcd/aansluiting.jpg)

## Bibliotheek

Om gebruik te kunnen maken van het scherm via de I2C-adapter is een Library (Bibliotheek) nodig. Dit is *niet* dezelfde als degene die al reeds is geïnstalleerd in Arduino IDE en zal dus nog toegevoegd moeten worden. Dit kan op de volgende manier:

**Bibliotheken beheren:** Druk op CTRL + Shift + I.

Of via het menu: 

>*Hulpmiddelen > Bibliotheken beheren...* 

Hier kun je zoeken naar `pcf8574 hertel`. Je vindt dan de [volgende bibliotheek](https://docs.arduino.cc/libraries/liquidcrystal_pcf8574/). 

![Bibliotheek_Hertel](/docs/assets/lcd/hertel_bibliotheek.png)

Klik vervolgens op _install_. Hierna is de bibliotheek geïnstalleerd en klaar om gebruikt te worden.

## De code

Wanneer je een (nieuwe) bibliotheek gebruikt om iets aan te sturen met een Arduino, is het noodzakelijk om de juiste code erbij te zoeken. Deze is meestal te vinden op de site van arduino zelf of anders op de site van de beheerder van de bibliotheek. In dit geval is de code slecht gedocumenteerd en zal ik hieronder dus een aantal voorbeelden geven.


### Hello World!

De code hieronder laat "Hello World!" op het scherm verschijnen. 


```c
#include <LiquidCrystal_PCF8574.h>
#include <Wire.h>

LiquidCrystal_PCF8574 lcd(0x27);

void setup() {
  lcd.begin(20,4);
  lcd.setBacklight(255);
  lcd.setCursor(0,0);
  lcd.print("Hello World!"); 
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

Voor het oproepen van een bibliotheek in een schets wordt `#include` gebruikt. Vervolgens staat de naam van de bibliotheek tussen `< >`. 
Een andere manier om een bibliotheek toe te voegen is door deze te kiezen vanuit het menu:

>*Schets > Bibliotheek gebruiken > ...*

Nieuwe geïnstalleerde bibliotheken staan meestal onderaan. 

In bovenstaand voorbeeld worden twee bibliotheken gebruikt:

* `<Wire.h>` - Dit is een bibliotheek voor I2C communicatie.
* `<LiquidCrystal_PCF8574.h>` - Dit is de nieuwe geïnstalleerde bibliotheek wat interactie met het LCD-scherm mogelijk maakt.

Vervolgens stellen het scherm in met `LiquidCrystal_I2C lcd(0x27)` waarbij `lcd` een variabele is om naar de bibliotheek te verwijzen en `0x27` het (standaard)adres is voor deze seriële communicatie. 

`lcd.begin(20,4)` geeft het aantal karakters per regel aan: 4 regels, 20 karakters per regel. 

`lcd.backlight(255)` zet de achtergrondverlichting aan.

`lcd.setCursor( kolom , rij )` zet de cursor op een specifieke plek. Linksboven is in dit geval positie `0,0`. Rechtsonder is `19,3`.

<!-- | 0,0 | 1,0 | 2,0 | 3,0 | 4,0 | 5,0 | 6,0 | 7,0 | 8,0 | 9,0 | 10,0 | 11,0 | 12,0 | 13,0 | 14,0 | 15,0 | 16,0 | 17,0 | 18,0 | 19,0 |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|------|------|------|------|------|------|------|------|------|------|
| 0,1 | 1,1 | 2,1 | 3,1 | 4,1 | 5,1 | 6,1 | 7,1 | 8,1 | 9,1 | 10,1 | 11,1 | 12,1 | 13,1 | 14,1 | 15,1 | 16,1 | 17,1 | 18,1 | 19,1 |
| 0,2 | 1,2 | 2,2 | 3,2 | 4,2 | 5,2 | 6,2 | 7,2 | 8,2 | 9,2 | 10,2 | 11,2 | 12,2 | 13,2 | 14,2 | 15,2 | 16,2 | 17,2 | 18,2 | 19,2 |
| 0,3 | 1,3 | 2,3 | 3,3 | 4,3 | 5,3 | 6,3 | 7,3 | 8,3 | 9,3 | 10,3 | 11,3 | 12,3 | 13,3 | 14,3 | 15,3 | 16,3 | 17,3 | 18,3 | 19,3 |
 -->
  
Vervolgens kan er geprint worden met `lcd.print()`. Als dit gaat om tekst (datatype: `String`) dan moet dit tussen aanhalingstekent `" "` staan.

Dit alles staat in de `void setup()` omdat dit alles slechts een keer wordt uitgevoerd. De `void loop()` is in dit geval dus leeg.


>[!NOTE] 
>Het kan zijn dat het scherm moeilijk leesbaar is doordat het te licht of te donker is. Dit kan bijgesteld worden door middel van een potmeter. Dit is het blauwe gedeelte op de I2C (zie foto bovenaan). Om dit bij te stellen kan er gebruik gemaakt worden van een kleine schroevendraaier.  

### Clear

Om het scherm leeg te maken wordt `lcd.clear()` gebruikt.

```c
#include <LiquidCrystal_PCF8574.h>
#include <Wire.h>

LiquidCrystal_PCF8574 lcd(0x27);

void setup() {
  lcd.begin(20,4);
  lcd.clear();
}

void loop() {

}
```