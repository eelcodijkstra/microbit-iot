# Wat heb je nodig?

:::{admonition} Lesmateriaal
Het bijbehorende keuzethema-lesmateriaal, bij het materiaal in deze cursus, vind je op: https://eelcodijkstra.github.io/netbook0/intro.html
:::

(benodigde-hardware)=
## Hardware

### microbit IoT-netwerk

:::{figure} figs/microbit-iot-network.drawio.png
:width: 600

micro:bit IoT netwerk, met IoT-nodes, gateway, en radio-logger
:::

Voor het IoT-netwerk **heb je de volgende onderdelen nodig**:

* *IoT-knoop(en)*: 1 of meer **microbits** V1 of V2 (voorkeur); voeding: batterij of USB. 
* *IoT-gateway*: **microbit V2 en Elecfreaks iot:bit bordje**; voeding: USB.
    *  bijv. via https://webshop.ictleskisten.nl/product/elecfreaks-iotbit-internet-wifi-extension-board-for-microbit-ef03426/
* *radio-logger*: **microbit** V1 of V2; voeding: via de host (USB)

De IoT-gateway verbindt het microbit IoT-netwerk met het internet, via het lokale (WiFi) netwerk.
De combinatie van microbit en iot:bit bordje heeft hiervoor een microbit-radio en een WiFi-radio, in de vorm van een ESP8266 WiFi module op de iot:bit.

Met de radio-logger (of *packet sniffer*) volg je het netwerkverkeer in het microbit IoT netwerk.
Deze microbit wordt verbonden met de host-computer voor de logging (Python print-opdrachten).
Deze host zorg ook voor de (USB) voeding van de microbit.

Naast de microbits heb je een laptop/desktop-computer nodig met een **recente Chrome of Edge browser**. Deze moet je via USB met een micro:bit kunnen verbinden.

:::{admonition} microbit V1: de juiste firmware?
Voor het gebruik van de online Python editor met een directe verbinding met de microbit (via WebUSB) heb je, naast de juiste browser, ook de juiste firmware voor de microbit nodig. Zie: https://microbit.org/get-started/user-guide/firmware/, voor de manier waarop je de versie controleert en zo nodig een nieuwe versie installeert. Je hebt versie 0243 of nieuwer nodig.
:::

Je kunt een IoT-knoop desgewenst van extra sensoren en actuatoren voorzien. Bijvoorbeeld: een elecfreaks octopus:bit bordje met een octopus PIR sensor en een octopus LED. 

**Minimale versie.** Je kunt met 1 micro:bit (V2) met een iot:bit bordje volstaan - maar je mist dan wel een deel van de *fun*.

**Absoluut minimale versie.** Je kunt de meeste opdrachten ook uitvoeren met gesimuleerde IoT-knopen - maar dan mis je nog meer van de *fun*.

### micro:bit V1 versus V2

:::{figure} figs/microbit-v1-v2-front.png
:width: 600

micro:bit versie 1 en versie 2 (voorkant)
:::

:::{figure} figs/microbit-v1-v2-back.png
:width: 600
micro:bit versie 1 en versie 2 (achterkant)
:::

Sinds oktober 2020 is de microbit V2 beschikbaar. Voor een overzicht van de verschillen tussen microbit versie 1 en versie 2, zie bijvoorbeeld: https://kitronik.co.uk/blogs/resources/explore-micro-bit-v1-microbit-v2-differences. Voor sommige functies in het microbit-IoT netwerk heb je deze versie 2 nodig, onder andere voor de gateway met het iot:bit bordje. Voor de meesta andere functies kun je eventueel met de oudere microbit V1 volstaan.

Voor het gebruik als IoT-knoop heeft versie 2 enkele belangrijke voordelen: (i) deze beschikt over *meer geheugen* (128kB RAM vs. 16 kB; 512 kB Flash vs. 256 kB), dit betekent dat je in Python veel minder snel geheugenproblemen krijgt, ook grotere programma's zijn mogelijk; (ii) je kunt deze in "low power sleep mode" zetten, om batterij-energie te sparen.

Daarnaast heeft V2 een aantal extra sensoren en actuatoren:

* touch sensor (6) op voorkant
* microfoon (7) op voorkant, (12) op achterkant
* luidspreker (11) op achterkant

En een extra led die aangeeft of de micro:bit "power" heeft (13 op de achterkant).

(benodigde-software)=
## Software

* recente Chrome of Edge browser (voor WebUSB in Python editor)
* online Python editor voor de microbit: https://python.microbit.org/v/3
    * alternatief: Python Mu desktop editor (https://codewith.mu)
* microbit Python programma's (in dit materiaal)
    * IoT-node software
    * radio-logger software
    * IoT-gateway software
* NodeRed (https://nodered.org); bijvoorbeeld via:
    * online versie: (via deze cursus, op basis van FlowForge)
    * op eigen computer geïnstalleerd
    * op Raspberry Pi, in lokale netwerk
* MQTT hulpprogramma's
    * MQTT broker (infvopedia:1883)
    * http://infvopedia.nl/mqt3.html
* gesimuleerde IoT-knoop
    * http://infvopedia.nl/iotnode-app.html
    
De MQTT broker (infvopedia.nl) gebruikt de Mosquitto software, zie: https://mosquitto.org. Deze kun je ook op een eigen computer, Raspberry Pi, enz., draaien. Voor de meeste IoT-toepassingen heb je een MQTT-broker nodig in het publieke internet. Een kleine cloud-server met Mosquitto is dan vaak voldoende.
 
(benodigd-netwerk)=
## Lokaal (WiFi) netwerk

De microbit IoT-gateway op basis van het iot:bit bordje maakt verbinding met het lokale WiFi netwerk; dit moet verbonden zijn met het internet.
Dit moet een netwerk zijn met een (enkel) netwerk-wachtwoord, zoals bijvoorbeeld een thuisnetwerk.
Een (school)netwerk met een gebruikersnaam en wachtwoord voor elke gebruiker is helaas niet mogelijk.

Enkele alternatieven voor een dergelijk schoolnetwerk: (i) een telefoon als tijdelijk WiFI access-point; (ii) een MiFi kastje: dit biedt een lokaal WiFi netwerk verbonden met het mobiele internet. Het mobiele dataverkeer is zeer beperkt, je kunt bijvoorbeeld kiezen voor een verbinding met lage snelheid ("2G").

Het lokale netwerk moet toegang tot de MQTT-broker mogelijk maken. (In sommige schoolnetwerken zijn erg veel niet-HTTP protocollen geblokkeerd. Ook dan biedt een MiFI kastje uitkomst.)

:::{note}
Er wordt nog gewerkt aan alternatieve gateway-implementaties voor gebruik in een schoolnetwerk, bijvoorbeeld op basis van een Raspberry Pi.
:::