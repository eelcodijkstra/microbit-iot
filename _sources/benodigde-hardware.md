# Wat heb je nodig?

(benodigde-hardware)=
## Hardware

* microbit-gateway:
    * microbit(V2)
    * Elecfreaks iot:bit bordje
        * bijv. https://webshop.ictleskisten.nl/product/elecfreaks-iotbit-internet-wifi-extension-board-for-microbit-ef03426/
    * gevoed via USB-voeding
* microbit-IoT-knoop(en):
    * microbit(bij voorkeur V2, eventueel V1)
    * zo mogelijk aangevuld met sensoren, bijvoorbeeld:
        * Elecfreaks octopus:bit bordje
        * octopus PIR sensor
        * octopus LED
    * gevoed uit batterij of uit USB
* microbit-logger:
    * microbit (V1 of V2)
    * verbonden met host-computer voor log-data
    
Daarnaast heb je een laptop/desktop-computer nodig met een recente Chrome of Edge browser. Deze moet je via USB met een micro:bit kunnen verbinden.

In principe kun je een microbit V1 gebruiken als IoT-knoop. Maar voor dit gebruik heeft versie 2 twee belangrijke voordelen: (i) je kunt deze goed in Python programmeren, door het extra geheugen; (ii) je kunt deze in "low power sleep mode" zetten, om batterij-energie te sparen.

**Minimale versie.** Je kunt met 1 micro:bit (V2) met een iot:bit bordje volstaan - maar je mist dan wel een deel van de *fun*.

(benodigde-software)=
## Software

* recente Chrome of Edge browser (voor WebUSB in Python editor)
* online Python editor voor de microbit: https://python.microbit.org/v/3
    * alternatief: Python Mu desktop editor (https://codewith.mu)
* microbit Python programma's (in dit materiaal)
* NodeRed; bijvoorbeeld via:
    * online versie: (via deze cursus, FlowForge)
    * op eigen computer geïnstalleerd
    * op Raspberry Pi, in lokale netwerk
* MQTT hulpprogramma's
    * MQTT broker (infvopedia:1883)
    * http://infvopedia.nl/mqt3.html
* gesimuleerde IoT-knoop
    * http://infvopedia.nl/iotnode-app.html
    
    
(benodigd-netwerk)=
## Netwerk

De microbit IoT-gateway op basis van het iot:bit bordje maakt verbinding met het lokale WiFi netwerk; dit moet verbonden zijn met het internet.
Dit moet een netwerk zijn met een (enkel) netwerk-wachtwoord, zoals bijvoorbeeld een thuisnetwerk.
Een (school)netwerk met een gebruikersnaam en wachtwoord voor elke gebruiker is niet mogelijk.

Enkele alternatieven voor een dergelijk schoolnetwerk: (i) een telefoon als tijdelijk WiFI access-point; (ii) een MiFi kastje: dit biedt een lokaal WiFi netwerk verbonden met het mobiele internet. Het mobiele dataverkeer is zeer beperkt, je kunt bijvoorbeeld kiezen voor een verbinding met lage snelheid ("2G").

Het lokale netwerk moet toegang tot de MQTT-broker mogelijk maken. (In sommige schoolnetwerken zijn erg veel niet-HTTP protocollen geblokkeerd. Ook dan biedt een MiFI kastje uitkomst.)