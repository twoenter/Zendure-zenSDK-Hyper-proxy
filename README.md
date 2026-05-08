# Zendure-zenSDK-Hyper-proxy
Wil je het maximale uit je Zendure thuisbatterij halen zonder afhankelijk te zijn van de cloud? Met deze slimme oplossing combineer je de kracht van de [Gielz-automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK) met een Hyper2000 — volledig lokaal aangestuurd via Home Assistant.

Hoewel de Gielz-automatisering oorspronkelijk alleen werkt met zenSDK-ondersteunde apparaten, maakt deze Node-RED flow het mogelijk om ook je Hyper2000 naadloos te integreren. De flow vertaalt automatisch de commando’s die normaal naar een SolarFlow 2400AC gaan, zodat jij profiteert van dezelfde geavanceerde automatisering — maar dan met jouw Hyper2000.

Meer controle, meer flexibiliteit, en vooral: geen afhankelijkheid meer van de Zendure cloud.
<img height="600" alt="image" src="https://github.com/user-attachments/assets/7d226f51-b008-4aa8-8c29-70a129223f79" />

## Compatibel met
Getest en werkend met:
- Hyper2000
- - AC Firmware v2.1.14
  - MASTER Firmware v2.1.30
  - BMS Firmware (AB2000) v1.0.17
  - ZenLink Master v3.1.14
  - ZenLink Secondary v3.1.14
- Zendure Home Assistant Integratie (Fireson) v1.2.5 [Zendure-HA integratie](https://github.com/Zendure/Zendure-HA)
- Gielz automatisering en package v20260507 [Gielz-automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK)

## Instructies Zendure Hyper2000 integratie in Home Assistant
- Installeer en configureer jouw Hyper2000 via de [Zendure-HA integratie](https://github.com/Zendure/Zendure-HA)
- Voor de beste prestaties zorg je voor lokale connectie via een bluetooth-proxy

<img height="250" alt="image" src="https://github.com/user-attachments/assets/a4d01e5a-ff99-416d-9a35-d0837e34253c" />


## Instructies Node-RED app
Installeer de [Node-Red Home-Assistant addon](https://github.com/hassio-addons/app-node-red) (tegenwoordig app). Stel het volgende in:

- Schakel "ssl" uit
- Schakel "Ongebruikte optionele configuratieopties tonen" in zodat je de volgende opties ziet:
- Schakel "leave_front_door_open" in
- Sla de configuratie op en (her)start Node-RED.
- Zet de optie 

## Instructies Node-RED Companion
- Installeer [Node-RED Home Assistant companion](https://github.com/zachowj/hass-node-red) via HACS
- Voeg de Node-Red companion integratie toe aan je integraties (niet overslaan)

## Configureer Gielz
- Importeer het [Gielz package](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#%EF%B8%8F%E2%83%A3-configuratie-en-herstart) in jouw configuration.yaml 
- Importeer de [Gielz automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#2%EF%B8%8F%E2%83%A3-zendure-zensdk-gielz-automatisering)
- Optioneel maar aanbevolen: importeer het [dashboard](https://github.com/Gielz1986/Zendure-HA-zenSDK/blob/main/README.nl.md#-optioneel-plug-n-play-dashboard)

## Configureer de zenSDK-Hyper-proxy
- Importeer in een nieuwe Node-red flow  de [zenSDK Hyper2000 GET flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20GET.json). Deze Node-red flow zorgt ervoor dat de informatie uit de Hyper naar de zendure entiteiten vertaald wordt voor de Gielz automatisering en dashboard.
- Importeer in een nieuwe Node-red flow de [zenSDK Hyper2000 POST flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20POST.json). Deze Node-red flow zorgt ervoor dat de waarden die de Gielz automatisering bepaald ook werkelijk naar de Hyper gecommuniceerd worden.    
### Pas in de GET flow het volgende aan:
 1. het aantal batterijen: verbind het juiste aantal batterijen door middel van de link nodes. Batterij 1 out link gaat naar Batterij 2 in en zo verder naar mate het aantal batterijen. Enable de nodes van de extra batterijen. De laatse out-node van de laatste batterij verbind je met de in-node 'Afronden update'. De volgorde in node-red hoeft niet te matchen met de volgorde in de stapel, dit kun je corrigeren in het gielz dashboard.
  <img width="1322" height="736" alt="image" src="https://github.com/user-attachments/assets/99ae2c12-bcb9-453d-90d2-8baaa6345896" />

  
 2. de serienummers van de batterijen en packType: Het serienummer wordt gebruikt door Gielz om onderscheid te maken tussen de batterijen en ze in de juiste gewenste volgorde te plaatsen. packType is de capaciteit van de accu, voor een AB2000s/x gebruik je 70, wat 1,92kWh is.
  <img height="200" alt="image" src="https://github.com/user-attachments/assets/24fa01a3-dc5d-4346-a1bf-5769a88259d7" />
  
 3. Verwijs in alle blauwe nodes van de batterijen naar de juiste entiteiten. De Zendure-HA integratie gebruikt standaard ``sensor.<<serienummer accu>>_power`` etc. Plak het juiste serienummer ertussen en het zal werken zolang je de standaard namen niet aangepast hebt.
  <img height="200" alt="image" src="https://github.com/user-attachments/assets/0328fe08-e63c-4524-a821-fc7db37b9f0c" />

  4. Het serienummer van de Hyper
     
     <img height="200" alt="image" src="https://github.com/user-attachments/assets/5c782333-07e6-4a34-86ce-17b148e2d811" />
     
### Pas in de POST flow het volgende aan
  1. In principe niets, check de juiste entiteitnamen van de Zendure-HA integratie
     
     <img height="200" alt="image" src="https://github.com/user-attachments/assets/6491f6a8-361e-4e73-af5c-1a40f9d6b129" />


## Configureer gielz (2)
- Stel in het gielz configuratie dashboard het ip-adres in van de Zendure op ``localhost:1880/endpoint``. Dit is het ip-adres van node red waardoor er connectie gelegd wordt tussen home assistant en node red. De twee beginnen over en weer te communiceren.
  <img width="416" height="150" alt="image" src="https://github.com/user-attachments/assets/7a99c900-75ce-4c2e-b85e-9c67c198581b" />
- Stel de juiste oplaad en ontlaad maximalen in, passend bij jouw situatie. 

## Gereed
De communicatie tussen Home Assistant en de Hyper2000 verloopt nu via Node-Red om gebruik te kunnen maken van de Gielz automatisering. Natuurlijk kun je altijd zelf de Hyper blijven aansturen, vergeet dan niet de gielz automatisering uit te schakelen, zodat er geen conflicterende opdrachten verzonden worden.

## Tips
In mijn ervaring is het beter om de rest ``scan_interval`` van de gielz automatisering van 1 naar 5 te verhogen, van veel verkeer naar de Hyper2000 schiet het nog wel eens in een freeze. Wanneer je een freeze ervaart, is de Hyper ogenschijnlijk nog online en bestuurbaar maar is dat in werkelijkheid niet. Commando's komen niet aan en worden niet uitgevoerd. Om een freeze te verhelpen kun je in de Fireson integratie klikken op Reset verbinding en/of de internetconnectie naar de Hyper even verbreken door in je router(app) even de verbinding naar de hyper te verbieden en na een aantal minuten weer toe te staan. 
  
