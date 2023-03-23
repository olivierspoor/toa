# RGB-LED

In deze les ga je werken met een RGB-LEDje. De opdracht bestaat uit drie onderdelen:

1. De drie kleuren afzonderlijk laten branden en knipperen.
2. De drie kleuren langzaam aan en uit laten gaan.
3. Het lampje de kleuren van de regenboog na laten bootsen.


## Het aansluiten van een RGB-LED

Voor deze opdracht heb je de volgende onderdelen nodig:

- RGB-LED
- 220 Ohm weerstand (3x)
- Verbindingsdraadjes (4x)

![rgb-led](../assets/images/rgb_led.png) 

Dit LED-lampje heeft 4 voetjes: rood, groen en blauw en een gemeenschappelijke cathode. Het langste voetje is de cathode (-) en sluit je aan op de grond (GND). De drie overige voetjes zijn de anodes en deze sluit je met een 220 Ohm weerstandje aan op een digitale pin met PWM~.  De volgorde van de drie kleuren kan wel eens afwijken van het voorbeeld. Dit zul je snel genoeg zien. 

## Pulse Width Modulation (PWM~)
In deze opdracht wil je de intensiteit van een lampje kunnen bepalen. De Arduino heeft enkel de mogelijkheid om 5 volt te genereren en kan de sterkte dus niet op deze manier beinvloeden. Daarom wordt er gebruikt gemaakt van een techniek: Pulse Width Modulation. PWM kan een pin heel snel aan- en uitzetten in een bepaalde tijd - sneller dan het menselijk ook kan zien. Dit wekt de indruk dat een lampje minder fel brandt. De verhouding tussen de tijd dat het lampje aan en uit is bepaald de intensiteit. 

![pwm](../assets/images/pwm.png)

Alle digitale pins op de Arduino kunnen een LED-lampje laten branden. Het langzaam aan en uit laten gaan is enkel mogelijk met deze speciale PWM-pin herkenbaar aan de ~ naast het nummer. De aansluiting ziet er als volgt uit.

![rgb-led-aansluiting](../assets/images/rgb_led_aansluiting.png)


## 1. Rood, Groen, Blauw afzonderlijk laten branden en knipperen.

Nu alles is aangesloten, kunnen we de Arduino gaan programmeren. We beginnen met het definieren van de constanten.


```arduino
const int pinBlauw=9;
```
Een niet te veranderen integer (getal) 9 wordt gelinkt met de naam 'pinBlauw'. Doe dit ook voor de andere kleuren.
Vervolgens kijken we naar de setup.

```arduino
void setup() {
  pinMode(pinBlauw, OUTPUT);
}
```
Het gedrag (*pinMode*) van de digitale pin met de naam *pinBlauw* (dat is dus pin 9) wordt ingesteld als *output*. 
Om nu het blauwe LEDje te laten branden heb je nog een stukje code nodig in de *void loop*:

```arduino
void loop() {
  digitalWrite(pinBlauw, HIGH);
}
```

Hiermee zeg je dat de digitale pin aangaat. Dit signaal is binair (heeft twee mogelijkheden): aan of uit, HIGH of LOW, 5 volt of 0 volt. 

Met deze informatie en met de kennis opgedaan uit de introductie zou je in staat moeten zijn om het lampje de drie kleuren achtereenvolgens te laten knipperen. Denk hierbij aan het gebruik van de ```delay()```, waarin je de tijd in miliseconden meegeeft.


<details>
<summary>Klik hier voor de oplossing</summary>

```arduino
const int pinBlauw=9;
const int pinGroen=10;
const int pinRood=11;

void setup() {
  pinMode(pinBlauw, OUTPUT);
  pinMode(pinGroen, OUTPUT);
  pinMode(pinRood, OUTPUT);
}

void loop() {
  digitalWrite(pinBlauw,HIGH);
  delay(500)
  digitalWrite(pinBlauw,LOW);
  delay(500)
  digitalWrite(pinGroen,HIGH);
  delay(500)
  digitalWrite(pinGroen,LOW);
  delay(500)
  digitalWrite(pinRood,HIGH);
  delay(500)
  digitalWrite(pinRood,LOW);
  delay(500)
}
```

</details>

## 2. Rood, Groen, Blauw langzaam aan en uit laten gaan.

De volgende stap is het varieren van de intensiteit van het LEDje. Hier gebruiken we ```analogWrite(pin, value)```, waarbij *pin* verwijst naar de anode van de kleur die je wilt aansturen en *value* de frequentie is van de PWM~ uitgedrukt in een waarde tussen de 0 (helemaal uit) en 255 (helemaal aan). 

Dit betekent dus dat ```digitalWrite(pinBlauw, HIGH)``` gelijk is aan ```analogWrite(pinBlauw, 255)```. 

Als we het lampje dus van uit (0) tot aan (255) willen laten gaan, moeten we de *value* langzaam laten toenemen. Hiervoor maken we gebruik van een `for` statement. Hiermee kunnen een blokje code herhalen tot er een bepaald eindpunt bereikt is.


## De `for` statement. 

Een `for` statement heeft de volgende syntax:
```arduino
for (initialization; condition; increment) {
  // statement(s);
}
```
Een `for` statement veronderstelt een bepaalde beweging; het laten toe- of afnemen van een waarde. *Initialization* is het vertrekpunt, een beginwaarde. *Condition* is de voorwaarde waaraan voldaan moet worden zolang de `for` statement actief is. *Increment* is de stapgrootte. De `{ }` omsluiten de code die tot de `for` statement behoren.

Dit passen we toe op ons lampje. De beginsituatie (*initialization*) is uit (0). Deze waarde willen we stapsgewijs laten toenemen (*increment*) tot deze 255 heeft bereikt (*condition*). Dit ziet er als volgt uit:

```arduino
for (int i = 0; i < 255; i=i+1) {
  analogWrite(pinBlauw, i);
  delay(50)
}
```
We definieren hier een integer *i* als variabele om de intensiteit bij te houden. Zolang deze kleiner is dan 255 mag deze in stapjes van 1 toenemen. De `delay()` is hier noodzakelijk omdat de Arduino dit zo snel uitvoert, dat het voor ons niet zichtbaar is. 

Met deze informatie zou je in staat moeten zijn het lampje ook langzaam uit te kunnen laten gaan. Denk daarbij goed aan wat je beginpunt is, de conditie en de richting van de stappen die je neemt. 

<details>
<summary>Klik hier voor de oplossing</summary>

```arduino
const int pinBlauw=9;
const int pinGroen=10;
const int pinRood=11;

void setup() {
  // De pinMode hoeft niet gespecificeerd te worden in combinatie met analogWrite.
}

void loop() {
  for (int i = 0; i < 255; i=i+1) {
    analogWrite(pinBlauw, i);
    delay(50)
  }
  for (int i = 255, i > 0; i=i-1) {
    analogWrite(pinBlauw, i);
    delay(50)
  }
  for (int i = 0; i < 255; i=i+1) {
    analogWrite(pinGroen, i);
    delay(50)
  }
  for (int i = 255, i > 0; i=i-1) {
    analogWrite(pinGroen, i);
    delay(50)
  }
  for (int i = 0; i < 255; i=i+1) {
    analogWrite(pinRood, i);
    delay(50)
  }
  for (int i = 255, i > 0; i=i-1) {
    analogWrite(pinRood, i);
    delay(50)
  }
}
```
Deze code kan korter en efficienter. Kijk hiervoor bij de extra opdrachten.

</details>


## 3. De kleuren van de regenboog.

Nu we weten hoe we de individuele kleuren kunnen aansturen, is het tijd om kleuren te gaan mengen. In de onderstaande afbeelding zien we de mengwaarden voor de kleuren van de regenboog.

![rgb_regenboog](../assets/images/rgb_regenboog.png)

Als we bijvoorbeeld paars willen maken (RGB(75,0,130)), dan geven we de RGB-waarden aan de lossen pins van het RGB-LEDje zoals in het onderstaande voorbeeld:

```arduino
const int pinBlauw=9;
const int pinGroen=10;
const int pinRood=11;

void setup() {

}

void loop() {
  analogWrite(pinRood, 75);
  analogWrite(pinGroen, 0);
  analogWrite(pinBlauw, 130);
}
```

De opdracht is om met bovenstaande informatie de kleuren van de regenboog langzaam voorbij te laten komen. Er zijn verschillende manieren om dit probleem op te lossen. Het is goed om van te voren te bedenken hoe je het probleem wilt aanpakken. Je kunt ook spelenderwijs ontdekken wat er gebeurd. 

<details>
<summary>Klik hier voor een hint</summary>

Als je kijkt naar de kleuren van de regenboog, kun je een patroon herkennen in de RGB-waarden. 

Bij de eerste drie kleuren is rood volledig aan. Bij kleur 2,3 en 4 is groen aan. En bij de laatste twee is blauw belangrijk. 

Je zou rood langzaam aan kunnen laten gaan. Vervolgens groen langzaam aan laten gaan, voordat je rood weer langzaam uit laat gaan. Enzovoort. 
</details>


<details>
<summary>Klik hier voor een mogelijke oplossing</summary>

```arduino
const int pinBlauw=9;
const int pinGroen=10;
const int pinRood=11;

// De intensiteit 
int iRood=0;
int iGroen=0;
int iBlauw=0;

void setup() {

}

void loop() {
  
  // rood langzaam aan
  for(iRood=0;iRood<255;iRood++){
    analogWrite(pinRood,iRood);
    delay(10);
  }
  
  // groen langzaam aan
  for(iGroen=0;iGroen<255;iGroen++){
    analogWrite(pinGroen,iGroen);
    delay(10);
  }
  
  // rood langzaam uit
  for(iRood=255;iRood>0;iRood--){
    analogWrite(pinRood,iRood);
    delay(10);
  }

  // blauw langzaam aan
  for(iBlauw=0;iBlauw<255;iBlauw++){
    analogWrite(pinBlauw,iBlauw);
    delay(10);
  }

  // groen langzaam uit
  for(iGroen=255;iGroen>0;iGroen--){
    analogWrite(pinGroen,iGroen);
    delay(10);
  }

  // rood langzaam aan
  for(iRood=0;iRood<255;iRood++){
    analogWrite(pinRood,iRood);
    delay(10);
  }

  // blauw en rood langzaam uit
  for(iRood=255;iRood>0;iRood--){
    analogWrite(pinRood,iRood);
    analogWrite(pinBlauw, iRood);
    delay(10);
  }

  delay(3000);
  

}
```
Deze code kan korter en efficienter. Kijk hiervoor bij de extra opdrachten.

</details>




## Woordenlijst

**RGB** - Rood, Groen, Blauw. In *additieve kleurmenging* zijn rood, groen en blauw de drie primaire kleuren die samen in verschillende combinaties en intensiteit de zichtbare kleuren kunnen uitdrukken. De hoeveelheid van elke primaire kleur die nodig is om de mengkleur te verkrijgen, wordt uitgedrukt in een getal dat meestal uit 8 bits bestaat (een waarde van 0 tot 255).

**LED** - *Light Emitting Diode*. Een soort diode dat oplicht wanneer er stroom door passeert. Zoals elke diode passeert de stroom slechts in een richting. 

**Diode** - Een diode is een elektronisch onderdeel dat de elektrische stroom zeer goed in een richting geleidt, maar praktisch niet in de andere. 

**Syntax** - 
