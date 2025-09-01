# Gebruiksaanwijzing

### opladen / vervangen batterijen
De herlaadbare 18500-batterijen worden opgeladen in de oplaadcase; bij het vervangen moet de robot niet in go mode staan.Dan de batterijen één voor één voorzichtig worden uitgenomen en correct volgens de polariteit teruggeplaatst worden op het oplaad case.”

### draadloze communicatie
#### verbinding maken
Voor draadloze communicatie tussen je GSM en de linefollower moet je eerst een verbinding maken met de HC-05 via Bluetooth. Log in met het wachtwoord 1234. Bij een volgende keer verbinden kan het nodig zijn de HC-05 eerst te ‘vergeten’ in je Bluetooth-instellingen. Zodra de Bluetooth-verbinding tot stand is gebracht, open je de app Serial Bluetooth Terminal en kies je het apparaat ‘HC-05’ (dit is het enige apparaat met een groen streepje ernaast)

#### commando's
Door help kan je alle beschikbare commando's zien
go : Hervat het volgen van de lijn
stop : stopt onmiddelijk
kal : 5s lang beweeg de sensor over zwart en wit
base=x : zet de basisrijsnelheid
kp=X : instellen van kp waarde
kd=X : instellen van kd waarde
gs=X : instellen van gs waarde
gamma=X : instellen van gamma waarde

### kalibratie
Met het commando kal start de robot een kalibratie van 5 seconden; beweeg tijdens die tijd de sensor over zowel zwart als wit. Met kal? kan je nadien de waarden voor zwart en wit bekijken
### settings
De robot rijdt stabiel met volgende parameters:
snelheid=200
kp=0.55
kd=0.6
gamma= 1.5


### start/stop button
Met de commando’s stop en go kan je via je GSM de wagen starten en stoppen; daarnaast kan je de auto ook laten stoppen met de resetknop op de Arduino zelf
