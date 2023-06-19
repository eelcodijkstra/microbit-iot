# Ontwerpen van een IoT-toepassing

Bij het ontwerpen van een IoT-toepassing heb je te maken met allerlei aspecten waarover je een ontwerp-beslissing moet nemen.

In het onderstaande gaan we uit van een IoT-toepassing met *eenvoudige sensoren*, met een lage data-rate: geen camera's of microfoons die een continue stroom beelden of geluiden moeten verwerken.
Dit betekent dat je met eenvoudige IoT-knopen kunt werken.
In veel gevallen kan zo'n IoT-knoop dan draadloos zijn en langere tijd op een (relatief kleine) batterij werken.

* welke sensoren heb je nodig?
    * welke gebeurtenis(sen) wil je kunnen detecteren?
* hoe vaak moet je meten?
* hoe snel moet je reageren op een bepaalde gebeurtenis?
* welke radio('s) kun je gebruiken?

## Sensoren

Niet voor elke toepassing heb je een direct passende sensor: soms kun je een bepaald fysisch verschijnsel het beste detecteren met een combinatie van sensoren. Dat kan ook de kans op vals alarm verkleinen.

Denk bijvoorbeeld aan een brand-detector: je kunt bijvoorbeeld een rookdetector combineren met een temperatuursensor en een infrarood-sensor.

Of een val-detector: je kunt een 3D versnellingsmeter combineren met een hoogtemeter (barometer).

Bij sensoren gaat het om twee zaken: signalen en events. 

Een signaal heeft op elk moment een waarde, denk bijvoorbeeld aan het signaal van een versnelling of van een temperatuur. 
Je hoeft dat signaal niet op elk moment te meten: een signaal verandert met een bepaalde snelheid, en je moet vaak genoeg meten om die veranderingen te kunnen waarnemen.

Denk aan de temperatuur in een kamer: deze zal per minuut niet meer dan 0,1 graad veranderen. Dat betekent dat je dan niet vaker dan eens per minuut hoeft te meten (en dat is waarschijnlijk nog aan de snelle kant.)


## Hoe vaak moet je meten?

## Hoe nauwkeurig moet je meten?

Begrippen (zie bijv. https://nl.wikipedia.org/wiki/Nauwkeurigheid)

* nauwkeurigheid of juistheid (accuracy, trueness): hoe goed benadert de gemeten waarde de werkelijke waarde?
* precisie of reproduceerbaarheid (precision): hoe dicht liggen verschillende metingen van eenzelfde waarde bij elkaar?
* (resolutie: aantal bits van de waarneming)
* (volgens ISO 5725 is *accuracy* de combinatie van *trueness* en *precision*)

Een sensor heeft een bepaalde nauwkeurigheid; bijvoorbeeld de meeste temperatuursensoren hebben een naukeurigheid van 0,5 of soms 0,1 graad Celcius.
Voor veel toepassingen, bijvoorbeeld het aansturen van de verwarming van een kamer, is een nauwkeurigheid van 0,5 graden voldoende. (Je kunt de precisie vergroten door te middelen over meerdere metingen.)

> De temperatuursensor van de microbit geeft de temperatuur op 1 graag nauwkeurig. Deze temperatuur wordt bij de processor gemeten, en kan dus enigszins afwijken.

Bij een analoge sensor heb je ook nog te maken met de resolutie van de A/D omzetter. Je kunt de resolutie van een A/D omzetter ten volle benutten als je ervoor zorgt dat het bereik van het meetsignaal en het bereik van de A/D omzetter ongeveer gelijk zijn.

N.B. hoewel een sensor een goede juistheid kan hebben, kan bijvoorbeeld de nabijheid van een warmtebron zoals een processor zorgen voor een systematische meetfout (en dus minder *juistheid*).

Voor veel sensoren wordt de gemeten waarde voorgesteld door een (geheel) getal van 10-12 bits. Een grotere nauwkeurigheid is fysisch lastig en/of duur.
Een nauwkeurige A/D omzetter voor geluid 

## Welke radio('s) kun je gebruiken?

De keuze voor een radio hangt onder andere af van:

* het bereik: lokaal (20 - 100m); grotere afstand (100m - enkele km's); globaal (bijv. landelijk dekkend; wereldwijd)
* het energieverbruik (batterijvoeding of netvoeding)
* de grootte van de berichten (en de frequentie daarvan).

Zie bijv. de onderstaande tabel:

| radio | bericht-grootte | bereik | energieverbruik |
| :---  | :---            | :---   | :---            |
| WiFi  | 1 kbyte         | 100m   | netvoeding (+)  |   
| BLE   | 20-100 byte     |  20m   | batterij        |
| LoRa  | 10-50 byte      | 2000m  | batterij        |

Voor gebruik in de huisomgeving zijn bijvoorbeeld WiFi, ZigBee en BLE geschikt. 

WiFi heeft een groter energieverbruik dan ZigBee en BLE, en is daardoor minder geschikt voor batterijgevoede apparaten. (WiFi kun je combineren met batterijvoeding als er zeer weinig berichten verstuurd worden, bijvoorbeeld in het geval van een personenweegschaal die tweemaal per dag een bericht stuurt.)

ZigBee en BLE zijn geschikt voor batterijvoeding, maar hebben een beperking op de grootte van de berichten.

De meeste LoRaWan netwerken hebben een grote (landelijke) dekking, soms zelfs wereldwijd. Als de lokale dekking minder goed is, kun je eenvoudig een eigen gateway toevoegen (The Things Network - TTN).

