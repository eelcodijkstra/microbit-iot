# LPP payload formaat


Voor het micro:bit IoT-netwerk gebruiken we het binaire Cayenne Low Power Payload formaat.
Dit formaat wordt ook in LoRaWan netwerken gebruikt; zie bijvoorbeeld: https://docs.mydevices.com/docs/lorawan/cayenne-lpp.

Daarnaast gebruiken we een vertaling van dit formaat naar het JSON-strings, om deze berichten via MQTT te verzenden.

:::{admonition} Standaard voor onze IoT-toepassingen
Voor de verschillende soorten IoT-knopen (WiFi, RF69, LoRaWan, micro:bit) gebruiken we niet alleen hetzelfde LPP-formaat, maar ook zoveel mogelijk dezelfde indeling van de kanalen voor de verschillende sensoren. De bijdehorende NodeRed flows zijn dan niet afhankelijk van de gebruikte IoT-knoop.
:::

Een pakket in het micro:bit IoT-netwerk begint met een **5-byte header**, gevolgd door de **payload in LPP formaat**. 

**Header:**

* 1 byte: protocol-ID (0x0A voor uplink-pakketten, van IoT-knoop naar gateway; 0x0B voor downlink-pakketten)
* 2 byte: node-ID (adres van afzender bij uplink cq. bestemming bij downlink)
* 2 byte: counter

De 2-byte getallen worden gegeven in de volgorde: hi byte, low byte. 

Een pakket bevat maar 1 adres, omdat het andere adres impliciet de gateway is, aangegeven door uplink of downlink. De IoT-nodes kunnen niet onderling communiceren.

**Payload:**

| channel | tag  | type        | data size | data resolution per bit| opmerking (microbit) |
| :---    | ---: | :---        | :---: | :---      | :---|
| 0       |  1   | dOut        | 1  | 1         | display, led0 (pin0)|
| 1       |  1   | dOut        | 1  | 1         | led1 (pin1)         |
| 2       |  0   | dIn         | 1  | 1         | button A            |
| 3       |  0   | dIn         | 1  | 1         | button B            |
| 4       |  103 | temperature | 2  | 0.1°C Signed MSB | microbit temperature |
| 5       |  115 | barometer   | 2  | 0.1 hPa Unsigned MSB | (gereserveerd) |
| 6       |  104 | humidity    | 1  | 0.5 % Unsigned | (gereserveerd) |
| 7       |  102 | presence    | 1  | 1         | shake, PIR sensor |
| 8       |  2   | aIn         | 2  | 0.01      | light level (display) |

De kanalen 5 en 6 zijn gereserveerd voor *barometer* en *humidity*.
In het geval van de micro:bit heb je daarvoor extra sensoren nodig.

> Bij andere IoT-knopen zijn *barometer* en *humidity* soms standaard aanwezig.

Als je andere sensoren of actuatoren toevoegt aan de microbit, dan moet je daarvoor kanalen 9 en hoger gebruiken, met een passende keuze voor het type.

**Voorbeeld van een pakket met header en payload in binair LPP formaat**

We geven dit als een rij bytes in Python-notatie.

```Python
[10, 59, 82, 1, 44, 0, 1, 0, 1, 1, 0, 2, 0, 0, 3, 0, 0, 4, 103, 1, 4, 8, 2, 0, 15]
```

**Voorbeeld van een pakket in JSON-LPP string-formaat**

Het bovenstaande binaire bericht met header en LPP-payload wordt in JSON:

```
{"nodeid": "3b52", 
 "counter": 300,
 "payload": {
     "4": {"temperature": 260}, 
     "8": {"aIn": 15}, 
     "1": {"dOut": 0}, 
     "0": {"dOut": 0}, 
     "3": {"dIn": 0}, 
     "2": {"dIn": 0}}}
 ```
 
 (Merk op dat de volgorde van de kanalen niet beslist gehandhaafd blijft in dit JSON-formaat.)