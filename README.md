# Optimiseur-solaire
## Changelog

- 06/12/2025 v0.0. initiale version.

## Description

Automatisation Home Assistant pour contrôler un équipement électrique en fonction du surplus de production solaire.  
Permet d’allumer l’équipement lorsque la consommation nette devient négative et de l’éteindre lorsque la consommation dépasse la puissance de l’équipement depuis un délai configurable.  

## Fonctionnalités

- Allumage automatique de l’équipement lors de surproduction solaire.  
- Extinction intelligente avec délai paramétrable pour éviter les toggles rapides.  
- Hystérésis configurable pour stabiliser les déclenchements autour des seuils de puissance.  
- 100% générique et réutilisable pour n’importe quel capteur ou switch.  

## Prérequis

- Home Assistant 2024 ou supérieur.  
- Capteurs de puissance (`sensor`) pour la consommation nette et la puissance de l’équipement.  
- Switch ou input_boolean pour contrôler l’équipement.  


## Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fcapof1000%2FOptimiseur-solaire%2Fblob%2Fmain%2Foptimiseur_binaire.yaml)



## Configuration

Le blueprint requiert les entrées suivantes (`!input`) :  

| Nom | Description |
|-----|-------------|
| `net_consumption` | Capteur de consommation nette du foyer (en W) |
| `equipment_switch` | Switch ou input_boolean de l’équipement à contrôler |
| `equipment_power` | Capteur de puissance de l’équipement (en W) |
| `hysteresis` | Marge pour éviter les allumages/extinctions trop rapides (W) |
| `delay_off` | Durée pendant laquelle la consommation doit rester au-dessus de la puissance de l’équipement avant extinction (secondes) |

## Exemple d’utilisation

```yaml
alias: "Optimisation chauffe-eau solaire"
use_blueprint:
  path: user/optimiseur-solaire.yaml
  input:
    net_consumption: sensor.consommation_nette_w
    equipment_switch: switch.chauffe_eau
    equipment_power: sensor.chauffe_eau_power
    hysteresis: 50
    delay_off: 10
