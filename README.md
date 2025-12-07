# Optimiseur-solaire
## Changelog

- 06/12/2025 v0.0. initiale version.

## Description

Automatisation Home Assistant visant a privileger l'auto-consommation de votre installation solaire en activant un équipement électrique pendant les periode de surplus de production solaire. 
Permet d’allumer de chauffer votre Cumulus d'eau chaude ( ou tout autre equipement electrique) lorsque la consommation nette devient négative et de l’éteindre lorsque la consommation dépasse la puissance de l’équipement depuis un délai configurable.  

## Fonctionnalités

- Allumage automatique de l’équipement lors de surproduction solaire.  
- Extinction intelligente avec délai paramétrable pour éviter les toggles rapides.  
- 100% générique et réutilisable pour n’importe quel capteur ou switch.  

 
## Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fcapof1000%2FOptimiseur-solaire%2Fblob%2Fmain%2Foptimiseur_binaire.yaml)

## Prérequis

- Home Assistant 2024 ou supérieur.  
- Switch ou input_boolean pour contrôler l’équipement. 
- Capteurs de puissance (`sensor`) mesurant la puissance utilisee par l’équipement commande.
- Capteurs de puissance (`sensor`) mesurant la consommation electrique globale ( pince shelly, lecteur Linky, etc...).  

## Configuration

Le blueprint requiert les entrées suivantes (`!input`) :  

| Nom | Description |
|-----|-------------|
| `net_consumption` | Capteur de consommation nette du foyer (en W) |
| `equipment_switch` | Switch ou input_boolean de l’équipement à contrôler |
| `equipment_power` | Capteur de puissance de l’équipement (en W) |
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
    delay_off: 60
