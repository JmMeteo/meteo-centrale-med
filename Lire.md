# Météo Centrale Méditerranée

Application web de bulletin météo interactif pour Centrale Méditerranée ( Campus de Marseille).

## Site en ligne

Le site est accessible ici :

https://JmMeteo.github.io/meteo-centrale-med/

## Objectif du projet

L'objectif est de créer un bulletin météo simple et dynamique permettant de visualiser les conditions météo actuelles, les prévisions et certains indicateurs environnementaux pour le campus de Centrale Méditerranée.

Ce projet permet également d'expérimenter :
- l'utilisation d'une API météo
- la récupération et le traitement de données en temps réel
- l'affichage dynamique dans une interface web
- l'hébergement via GitHub Pages

L'objectif ultime est de pouvoir joindre les datas de la station météo du campus.

## Localisation

Les données météo correspondent à la position du campus :

Latitude : 43.341000  
Longitude : 5.438472  
Fuseau horaire : Europe/Paris

## Technologies utilisées

- HTML
- CSS
- JavaScript
- API Open-Meteo
- GitHub Pages

## Données récupérées

Le projet récupère notamment les indicateurs suivants :

- température
- température ressentie
- humidité relative
- pression atmosphérique
- vitesse du vent
- direction du vent
- rafales de vent
- précipitations
- couverture nuageuse
- visibilité
- indice UV
- rayonnement solaire
- qualité de l'air (AQI)

## Fonctionnalités

- affichage de la météo actuelle
- prévisions horaires
- prévisions sur plusieurs jours
- indicateurs environnementaux
- mise à jour automatique des données
- interface dynamique (météo et cycle du jour)

## Fréquence de mise à jour

- récupération des données météo : toutes les 5 minutes
- rafraîchissement de l'affichage : toutes les 60 secondes

## Structure du projet

meteo-centrale-med/

index.html  
script.js  
README.md

## Source des données

Les données proviennent de l’API Open-Meteo  
https://open-meteo.com/

