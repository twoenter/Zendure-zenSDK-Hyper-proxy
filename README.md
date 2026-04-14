# Zendure-zenSDK-Hyper-proxy
Wil je het maximale uit je Zendure thuisbatterij halen zonder afhankelijk te zijn van de cloud? Met deze slimme oplossing combineer je de kracht van de [Gielz-automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK) met een Hyper2000 — volledig lokaal aangestuurd via Home Assistant.

Hoewel de Gielz-automatisering oorspronkelijk alleen werkt met zenSDK-ondersteunde apparaten, maakt deze Node-RED flow het mogelijk om ook je Hyper2000 naadloos te integreren. De flow vertaalt automatisch de commando’s die normaal naar een SolarFlow 2400AC gaan, zodat jij profiteert van dezelfde geavanceerde automatisering — maar dan met jouw Hyper2000.

Meer controle, meer flexibiliteit, en vooral: geen afhankelijkheid meer van de Zendure cloud.

## Instructies Zendure Hyper2000 integratie in Home Assistant
Installeer en configureer jouw Hyper2000 via de [Zendure-HA integratie](https://github.com/Zendure/Zendure-HA)

## Instructies Node-RED app
Installeer de [Node-Red Home-Assistant addon](https://github.com/hassio-addons/app-node-red) (tegenwoordig app). Stel het volgende in:

- Schakel "ssl" uit
- Schakel "Ongebruikte optionele configuratieopties tonen" in zodat je de volgende opties ziet:
- Schakel "leave_front_door_open" in
- Sla de configuratie op en (her)start Node-RED.

## Instructies Node-RED Companion
- Installeer [Node-RED Home Assistant companion](https://github.com/zachowj/hass-node-red) via HACS
- Voeg de Node-Red companion integratie toe aan je integraties (niet overslaan)

## Configureer Gielz
- Importeer het [Gielz package](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#%EF%B8%8F%E2%83%A3-configuratie-en-herstart) in jouw configuration.yaml 
- Importeer de [Gielz automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#2%EF%B8%8F%E2%83%A3-zendure-zensdk-gielz-automatisering)
- Optioneel maar aanbevolen: importeer het [dashboard](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#-optioneel-plug-n-play-dashboard)

## Configureer de zenSDK-Hyper-proxy

- Importeer in een nieuwe Node-red flow  de [GET flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20GET). Deze Node-red flow zorgt ervoor dat de informatie uit de Hyper naar de zendure entiteiten vertaald wordt voor de Gielz automatisering en dashboard.
- Importeer in een nieuwe Node-red flow de [WRITE flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20POST.json). Deze Node-red flow zorgt ervoor dat de waarden die de Gielz automatisering bepaald ook werkelijk naar de Hyper gecommuniceerd worden.    
- Pas in de GET flow het volgende aan:
-- het aantal batterijen
-- de serienummers van de batterijen en hyper

- Pas in de POST flow het volgende aan:
-- niets! 

In principe zijn alle standaard namen gebruikt zoals de Zendure-Ha integratie ze aanmaakt, maar kijk ze voor de zekerheid na. 

## Configureer gielz (2)
- Stel in het gielz configuratie dashboard het ip-adres in van de Zendure op 
``localhost:1880/endpoint``. Dit is het ip-adres van node red waardoor er connectie gelegd wordt tussen home assistant en node red. De twee beginnen over en weer te communiceren. 
