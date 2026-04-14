# Zendure-zenSDK-Hyper-proxy
Wil je het maximale uit je Zendure thuisbatterij halen zonder afhankelijk te zijn van de cloud? Met deze slimme oplossing combineer je de kracht van de [Gielz-automatisering](https://github.com/Gielz1986/Zendure-HA-zenSDK) met een Hyper2000 — volledig lokaal aangestuurd via Home Assistant.

Hoewel de Gielz-automatisering oorspronkelijk alleen werkt met zenSDK-ondersteunde apparaten, maakt deze Node-RED flow het mogelijk om ook je Hyper2000 naadloos te integreren. De flow vertaalt automatisch de commando’s die normaal naar een SolarFlow 2400AC gaan, zodat jij profiteert van dezelfde geavanceerde automatisering — maar dan met jouw Hyper2000.

Meer controle, meer flexibiliteit, en vooral: geen afhankelijkheid meer van de Zendure cloud.
<img height="600" alt="image" src="https://github.com/user-attachments/assets/7d226f51-b008-4aa8-8c29-70a129223f79" />


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
- Importeer in een nieuwe Node-red flow  de [zenSDK Hyper2000 GET flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20GET). Deze Node-red flow zorgt ervoor dat de informatie uit de Hyper naar de zendure entiteiten vertaald wordt voor de Gielz automatisering en dashboard.
- Importeer in een nieuwe Node-red flow de [zenSDK Hyper2000 POST flow](https://github.com/twoenter/Zendure-zenSDK-Hyper-proxy/blob/main/zenSDK%20Hyper2000%20POST.json). Deze Node-red flow zorgt ervoor dat de waarden die de Gielz automatisering bepaald ook werkelijk naar de Hyper gecommuniceerd worden.    
### Pas in de GET flow het volgende aan:
 1. het aantal batterijen: kopieer de nodes van batterij 2 (soc, power, state en maxTemp) door naar 3 en verder, zorg dat ze op dezelfde manier verbonden worden. De link node komt als laatste aan de laatste batterij
  <img height="200" alt="image" src="https://github.com/user-attachments/assets/01f6f2af-3429-4169-a542-1229d60e4faa" />
  
 2. de serienummers van de batterijen en packType: Het serienummer wordt gebruikt door Gielz om onderscheid te maken tussen de batterijen en ze in de juiste gewenste volgorde te plaatsen. packType is de capaciteit van de accu, voor een AB2000s/x gebruik je 70, wat 1,92kWh is.
  <img height="200" alt="image" src="https://github.com/user-attachments/assets/24fa01a3-dc5d-4346-a1bf-5769a88259d7" />
  
 3. Verwijs in alle blauwe nodes van de batterijen naar de juiste entiteiten. De Zendure-HA integratie gebruikt standaard ``sensor.<<serienummer accu>>_power`` etc. Plak het juiste serienummer ertussen en het zal werken.
  <img height="200" alt="image" src="https://github.com/user-attachments/assets/0328fe08-e63c-4524-a821-fc7db37b9f0c" />

  4. Het serienummer van de Hyper
     <img height="200" alt="image" src="https://github.com/user-attachments/assets/5c782333-07e6-4a34-86ce-17b148e2d811" />
     
### Pas in de POST flow het volgende aan
  1. In principe niets, check de juiste entiteitnamen van de Zendure-HA integratie
     <img height="200" alt="image" src="https://github.com/user-attachments/assets/6491f6a8-361e-4e73-af5c-1a40f9d6b129" />


## Configureer gielz (2)
- Stel in het gielz configuratie dashboard het ip-adres in van de Zendure op ``localhost:1880/endpoint``. Dit is het ip-adres van node red waardoor er connectie gelegd wordt tussen home assistant en node red. De twee beginnen over en weer te communiceren. <img width="644" height="469" alt="image" src="https://github.com/user-attachments/assets/e479218f-39f0-40f9-8948-de0be83d8116" />
- Stel de juiste oplaad en ontlaad maximalen in, passend bij jouw situatie. 

## Gereed
De communicatie tussen Home Assistant en de Hyper2000 verloopt nu via Node-Red om gebruik te kunnen maken van de Gielz automatisering. Natuurlijk kun je altijd zelf de Hyper blijven aansturen, vergeet dan niet de gielz automatisering uit te schakelen, zodat er geen conflicterende opdrachten verzonden worden.
  
