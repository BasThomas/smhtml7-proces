# Proces

## Switch van Google Places naar Wikipedia API
We waren van plan de API van Google Places te gebruiken om interessante bezienswaardigheden op te halen en in de app weer te geven. Na daar kort onderzoek naar te hebben gedaan, bleek het niet helemaal passen:

- Het ophalen van alleen "bezienswaardigheden" was niet mogelijk.
- Het ophalen van verschillende categorieën ook niet.
- De data was daardoor incompleet en onoverzichtelijk.

Zoekende naar een alternatief stuitten we op de Wikipedia API. Hiermee was het mogelijk artikelen, gekoppeld aan coördinaten, op te halen. Sterker nog: het was mogelijk dit in een radius om een ander coördinaat te doen! Ideaal.

## Wikipedia API: Engels naar Nederlands
De Engelse API van Wikipedia werkte in principe prima; maar het leek ons interessant eens te kijken wat de verschillen in resultaat waren tussen de twee. De Engelse API gaf natuurlijk alleen Engelse pagina's terug; de Nederlandse - je raadt het al - Nederlandse. En dat is waar wij resultaten wilden hebben! Het bleek dan ook dat met de Nederlandse API meer resultaten werden gevonden, alsook betere beschrijvingen van de plaatsen. De keuze was toen snel gemaakt.

Het is hiermee ook interessant, wanneer de app verder zou worden uitgebreid, de Wikipedia taal / API te baseren op de huidige locatie. Dan heb je van bovenstaande verbeteringen wereldwijd profijt! Al zal het natuurlijk handig zijn als je alsnog een taal aan kunt geven; als Nederlander wordt het in Rusland met Russische resultaten toch wat lastig.

# Hoe we foto's uploaden
Toen we het uploaden van foto's toevoegde aan de app, bleek dat we van de foto-picker geen image data kregen, maar een lokaal (tijdelijk) pad naar de foto. Onhandig. Zeker als we willen uploaden: hoe gaan we dat doen? En wat als we straks de app opnieuw openen, maar het tijdelijke pad niet meer bestaat?

Omdat we de koppeling met een backend hebben, hebben we ervoor gekozen om daar optimaal gebruik van de maken. Het is ook de bedoeling dat daar de foto's te bekijken zijn. Wat is dan de handigste optie? Ons leek het praktisch de foto te uploaden, en vervolgens een `permalink` terug te sturen. Daarmee voorkwamen we dat:

- er een afhankelijkheid van (tijdelijke) lokale adressen zou zijn;
- en we hoeven geen (`base64`) fotodata op te slaan (waarmee we een hoop ruimte besparen op het device).
