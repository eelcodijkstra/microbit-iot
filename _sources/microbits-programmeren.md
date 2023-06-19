# Programmeren van de micro:bits

De onderstaande handleiding gaat uit van de [online Python editor](https://python.microbit.org/v/3/) voor het programmeren van de micro:bits.

Als alternatief voor de online editor kun je een desktop editor als Mu gebruiken.
De aanwijzingen daarvoor zijn nog niet in detail uitgewerkt.

Voor het kopiëren van de code uit de tekst gebruik je de "Copy" knop rechtsboven in het betreffende code-blok.

(iot-knoop-programmeren)=
## Programmeren van de IoT-knopen

* selecteer in de Python editor, in de linker zijbalk, de tab "Project"
* klik links in de Python-editor op `main.py`
* kopieer de {ref}`iot-node-code` over de bestaande code in het (middelste) code-venster.
* test deze software: bij het verzenden krijg je de bytes van het verzonden bericht te zien (via de "serial" host-USB verbinding, in het "serial" venster onder de code in de editor).

Deze versie gebruikt alleen de ingebouwde sensoren en actuatoren; maar je kunt eventueel een LED aansluiten op pin0, deze werkt parallel aan het display.

(radio-logger-programmeren)=
## Programmeren van de radio-logger

De radio-logger gebruikt een extra module, deze moet je eerst laden in de online Python editor.

* selecteer in de Python editor, in de linker zijbalk, de tab "Project"
* klik links op "Create file", en vul als naam in: `lppjson`
* kopieer de {ref}`lppjson-module-code` naar het (middelste) code-venster
* klik links in de Python-editor op `main.py`
* kopieer de {ref}`radio-logger-code` naar het code-venster
* test de software, in combinatie met een IoT-knoop microbit: je krijgt dan de bytes van de ontvangen berichten te zien (via de "serial" host-USB verbinding).

(gateway-programmeren)=
## Programmeren van de micro:bit als gateway

De gateway bestaat uit een iot:bit bordje met daarin een micro:bit V2(!).

:::{Warning}
Haal voor het programmeren de micro:bit uit het iot:bit bordje. 
Je mag de micro:bit niet tegelijk met de host verbinden en met het iot:bit bordje.
:::

Verbind de micro:bit met de host en start de Python editor op.

Het gateway-programma gebruikt drie extra modules, deze moet je eerst laden in de online Python-editor.

* selecteer in de Python editor, in de linker zijbalk, de tab "Project"
* klik links op "Create file", en vul als naam in: `espat`
* kopieer de {ref}`espat-module-code` code naar het (middelste) code-venster
* klik links op "Create file", en vul als naam in: `ulpp`
* kopieer de {ref}`ulpp-module-code` naar het code-venster
* klik links op "Create file", en vul als naam in: `json`
* kopieer de {ref}`json-module-code` naar het code-venster

Vervolgens kopieer je de gateway-code en past deze aan voor je eigen netwerk:

* klik links in de editor op `main.py`
* kopieer de {ref}`gateway-code` naar het code-venster

Je moet in de gekopieerde gateway-code de WiFi-ssid-(netwerknaam) en -wachtwoord-strings aanpassen met de waarden van je eigen WiFi-netwerk. De onderstaande waarden werken waarschijnlijk niet in jouw omgeving:

```
wifi_ssid = 'infvo-iot'
wifi_password = 'LISP77(Midas'
```

De mqtt-waarden kun je onveranderd laten.

* klik op "Send to micro:bit" in het midden, en volg de aanwijzingen.

Je hebt nu de micro:bit geprogrammeerd, en kunt deze verbinden met de iot:bit.

* Maak de micro:bit los van de host-verbinding, en plaats deze (met het display naar boven) in het iot:bit bordje.
* Sluit de USB-voeding aan op de iot:bit (aan de zijkant), en zet de iot:bit aan.

De micro:bit start nu op, probeert verbinding te maken met het lokale WiFi netwerk, en daarna met de MQTT-broker. Je kunt de status volgen op het display en via de radio-logger micro:bit.

* 0: opstarten van gateway-code
* 1: ESP-module gevonden
* 2: WiFi verbinding gemaakt
* M: MQTT verbinding gemaakt

Steeds als je de micro:bit reset of als je de power inschakelt, doorloopt de micro:bit deze stappen.

Als de gateway verbinding heeft met de MQTT-broker ("M" op het display), dan kun je de berichten van de lokale IoT-knoop-microbit(s) ontvangen in de mqt3-app, in de dashboard-app, en in NodeRed. Je kunt dit testen door op één van de knoppen van de IoT-knoop te drukken.

Als een IoT-knoop tenminste één bericht verstuurd heeft via de gateway, kun je ook berichten vanuit mqt3 of NodeRed naar deze IoT-knoop sturen.
