# zolertia# Architecture de réseaux IoT

## Getting Started

### Configuration Border-Router && CoaP server

Ouvrir votre VM Linux<br>
Brancher la zolertia border-router puis la zolertia CoaP server<br>
Ouvrir 2 terminaux<br><br>

Paramétrage du Border-router :<br>
  * `cd workspace/ECE/examples/ipv6/rpl-boreder-router`
  * `sudo make border-router.upload PORT=/dev/ttyUSB0`
  * `sudo make connect-router PREFIX=2001:abcd:bafa:bafa::1/64 PORT=/dev/ttyUSB0`

Paramétrage du CoaP server :<br>
  * `cd workspace/ECE/examples/er-rest-example`
  * `sudo make er-example-server.upload PORT=/dev/ttyUSB1`
  * `sudo make login PORT=/dev/ttyUSB1`

### Récupération et Affichage des valeurs du Light sensor
Etape               | Action
:--------------------|:-------------------------
1                   | Ouvrir Mozilla [Doc: mozilla.org](https://www.mozilla.org/fr/)
2                   | Nouvel Onglet [Doc: [Adresse du border-router]]([Adresse du border-router])
3                   | Nouvel Onglet [Doc: coap://[Adresse de la passerelle]](coap://[Adresse de la passerelle])
4                   | Cliquer sur Discover
5                   | Cliquer sur la ressource Light-sensor
6                   | Cliquer sur la requête GET

## Programme

L'initialisation du timer:<br>
  * Initialisation `etimer_set(&et, CLOCK_SECOND*SECONDS)`
  * Expiration `etimer_expired(&et)`
  * Reset `etimer_reset(&etS)`

L'initialisation et l'affectation du relai:<br>
  * Ajout de la librairie `#include "dev/relay.h"`
  * Définition et activation `relay.value(RELAY_ON)` ou `relay.value(RELAY_OFF)`

Ajout d'une nouvelle ressource Light-sensor:<br>
  * Initialisation: `RESOURCE(res_light_sensor,
                        "title=\"light status\";rt=\"light"",
                        res_get_handler,
                        NULL,
                        NULL,
                        NULL);`
  * Activation: `rest_activate_resource(&res_light_sensor, "test/light_sensor")`

## Version
La version actuel : `1.0.0`

## Contributors
Maxime CAZADE & Vincent BAS
