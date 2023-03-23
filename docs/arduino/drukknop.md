# Drukknoppen

Drukknoppen verbinden twee punten in een stroomkring wanneer ze ingedrukt worden. Zo kun je ze bijvoorbeeld gebruiken om een LED-lampje aan te laten gaan zoals in het voorbeeld hieronder.

![LED met drukknop in stroomkring](../assets/images/Drukknop_LED.png)

De stroomkring wordt fysiek onderbroken door de drukknop. Enkel wanneer de knop ingedrukt is, is de stroomkring compleet en brandt het LEDje. 


Er zijn verschillende drukknopjes. Sommigen hebben twee pootjes, anderen hebben er vier - zoals in het voorbeeld hieronder. Hierbij is het belangrijk om te weten op welke manier de knop geplaatst moet worden.

![drukknop](../assets/images/drukknop.png)


Drukknoppen hebben dus twee standen. Wanneer we een drukknop verbinden met een Arduino geeft dit verschillende mogelijkheden. Een Arduino kan namelijk de stand van een knop lezen. Dit principe werkt hetzelfde: de knop onderbreekt een stroomkring die gesloten kan worden door de knop in te drukken. 

Een drukknop kan gelezen worden door deze te verbinden aan een digitale pin. Deze pin leest de stand van de drukknop als `HIGH` of `1`, ofwel als `LOW` of `0`.

![drukknop lezen](../assets/images/digitalRead_drukknop.png)

```arduino
int drukknop = 2;

void setup() {
  Serial.begin(9600);
  pinMode(drukknop, INPUT);
}

void loop() {
  int knopStatus = digitalRead(drukknop);
  Serial.println(knopStatus);
  delay(10);
}
```

![drukknop inputpullup lezen](../assets/images/Drukknop_InputPullup.png)


![drukknop lezen LED schrijven](../assets/images/Drukknop_InputPullup_LED.png) 
