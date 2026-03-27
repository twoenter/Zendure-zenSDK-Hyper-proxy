# Zendure-zenSDK-Hyper-proxy
Maak gebruik van de Gielz-automatisering voor Zendure thuisbatterijen in combinatie met een Hyper2000 in plaats van een zenSDK ondersteund apparaat. Alles verloopt 100% lokaal via Home Assistant. Je bent niet afhankelijk van de verbinding met de Zendure cloud. De Gielz-automatisering werkt alleen met één Zendure apparaat met zenSDK ondersteuning.

Met deze NODE-RED flow kun je de gielz-automatisering gebruiken met je Hyper2000. De NODE-RED flow zorgt voor de vertaling van de commando's die de gielz automatisering normaliter verzend naar de SolarFlow 2400ac.

## Instructies Node-RED

Installeer de NODE-RED Home-Assistant addon (tegenwoordig app). 
In de nodered flow hoef je verder niets in te stellen, wellicht alleen aan te passen naar jouw eigen entiteitnamen. 

Hiervoor importeer je eerst de flow Zendure-proxy-Node-Red-flow.json in Node-RED via het menu (hamburger rechtsboven) -> Import. Vervolgens open je het blok "Vul hier de Zendure IP adressen in" door erop te dubbel clicken. Na invullen van de IP adressen click je op "Done". Daarna click je op de "Deploy" knop rechts boven in Node-RED om de flow te activeren. Daarmee is de Node-RED kant gereed.
