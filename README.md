# Proces

## Userstories op Trello
Om voor al onze userstories bij te houden wat de status van deze userstorie was en wat eventuele deeltaken van deze userstorie waren hebben we gebruik gemaakt van Trello. Wij hebben voor Trello gekozen omdat dit een gratis online platform is dat makkelijk en snel te gebruiken is. Trello is een agileboard waar je userstories kan aanmaken en deze kunt opdelen in taken. Ook is het mogelijk om iedere userstorie een of meerdere tags te geven. Deze tags hebben wij gebruikt om aan te geven in welke sprint we de userstorie gingen realiseren en welke prioriteit deze had. Ook hebben we in Trello aangegeven wie aan welke taak bezig was zodat dit niet door elkaar ging lopen.

## Switch van Google Places naar Wikipedia API
We waren van plan de API van Google Places te gebruiken om interessante bezienswaardigheden op te halen en in de app weer te geven. Na daar kort onderzoek naar te hebben gedaan, bleek het niet helemaal passen:

- Het ophalen van alleen "bezienswaardigheden" was niet mogelijk.
- Het ophalen van verschillende categorieën ook niet.
- De data was daardoor incompleet en onoverzichtelijk.

Zoekende naar een alternatief stuitten we op de Wikipedia API. Hiermee was het mogelijk artikelen, gekoppeld aan coördinaten, op te halen. Sterker nog: het was mogelijk dit in een radius om een ander coördinaat te doen! Ideaal.

## Wikipedia API: Engels naar Nederlands
De Engelse API van Wikipedia werkte in principe prima; maar het leek ons interessant eens te kijken wat de verschillen in resultaat waren tussen de twee. De Engelse API gaf natuurlijk alleen Engelse pagina's terug; de Nederlandse - je raadt het al - Nederlandse. En dat is waar wij resultaten wilden hebben! Het bleek dan ook dat met de Nederlandse API meer resultaten werden gevonden, alsook betere beschrijvingen van de plaatsen. De keuze was toen snel gemaakt.

Het is hiermee ook interessant, wanneer de app verder zou worden uitgebreid, de Wikipedia taal / API te baseren op de huidige locatie. Dan heb je van bovenstaande verbeteringen wereldwijd profijt! Al zal het natuurlijk handig zijn als je alsnog een taal aan kunt geven; als Nederlander wordt het in Rusland met Russische resultaten toch wat lastig.

## Hoe we foto's uploaden
Toen we het uploaden van foto's toevoegde aan de app, bleek dat we van de foto-picker geen image data kregen, maar een lokaal (tijdelijk) pad naar de foto. Onhandig. Zeker als we willen uploaden: hoe gaan we dat doen? En wat als we straks de app opnieuw openen, maar het tijdelijke pad niet meer bestaat?

Omdat we de koppeling met een backend hebben, hebben we ervoor gekozen om daar optimaal gebruik van de maken. Het is ook de bedoeling dat daar de foto's te bekijken zijn. Wat is dan de handigste optie? Ons leek het praktisch de foto te uploaden, en vervolgens een `permalink` terug te sturen. Daarmee voorkwamen we dat:

- er een afhankelijkheid van (tijdelijke) lokale adressen zou zijn;
- en we hoeven geen (`base64`) fotodata op te slaan (waarmee we een hoop ruimte besparen op het device).

## Extern filesysteem
Op de server slaan we de foto's niet op in de database. Alleen een referentie ernaar. De foto's zelf uploaden we in een filesysteem: het zijn tenslotte files. Dit zorgt ervoor dat de database "klein" en snel blijft.

## Native Google Maps in plaats van JS Google Maps
We hebben ervoor gekozen de native Google Maps te gebruiken, in plaats van de JS Google Maps. De reden daarvoor is simpel: daarmee voelt de map native aan. In de JS API wordt gebruik gemaakt van de Maps zoals je die op een website ziet; dat is niet iets wat je wilt zien in een app.

Daarbij is de native API efficiënter / sneller te laden. Zeker met de tragere (Android) devices die we gebruiken, is dit geen slechte (bijkomende) eigenschap.

## Search by name -> Search by coordinates
Op de website worden naast de foto's, ook een map getoond van de plaats waar de foto's zijn gemaakt. Dat zijn Google Maps. In eerste instantie werden deze opgehaald aan de hand van namen van bezienswaardigheden; maar omdat Google Maps niet van alle Wikipedia-pagina's op de hoogte is, gaf deze het soms op en werd er geen marker getoond. Je zag gewoon de wereldbol.

Omdat dit geen fijne gebruikerservaring is, zijn we in plaat van de namen, de kaarten gaan tonen op basis van "hardcoded" coördinaten - die uiteraard werden meegegeven vanuit de Wikipedia API / de app. Win-win!

## Efficiënt API-gebruik
Er is stilgestaan bij dataverbruik van gebruikers - en gewoon "wat logisch is" - bij het ophalen van informatie met behulp van een API. Zo wordt bij het overzicht van bezienswaardigheden alleen de naam en bijhorende coördinaten opgehaald - pas als de gebruiker de locatie opslaat, wordt de overige informatie (lees: de introtekst van Wikipedia) opgehaald. Daarmee wordt er geen data verbruikt wanneer dat niet nodig is, en zou de applicatie in theorie ook nog iets sneller moeten zijn.
