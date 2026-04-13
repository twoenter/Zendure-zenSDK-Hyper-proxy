# Zendure-zenSDK-Hyper-proxy
Wil je het maximale uit je Zendure thuisbatterij halen zonder afhankelijk te zijn van de cloud? Met deze slimme oplossing combineer je de kracht van de [Gielz-automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK) met een Hyper2000 — volledig lokaal aangestuurd via Home Assistant.

Hoewel de Gielz-automatisering oorspronkelijk alleen werkt met zenSDK-ondersteunde apparaten, maakt deze Node-RED flow het mogelijk om ook je Hyper2000 naadloos te integreren. De flow vertaalt automatisch de commando’s die normaal naar een SolarFlow 2400AC gaan, zodat jij profiteert van dezelfde geavanceerde automatisering — maar dan met jouw Hyper2000.

Meer controle, meer flexibiliteit, en vooral: geen afhankelijkheid meer van de Zendure cloud.

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

- Importeer in een nieuwe flow de [GET flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20GET) 

