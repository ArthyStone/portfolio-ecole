---
title: "ScreenShow"
date: 2025-06-01
cadre: "Projet Personnel"
resume: "Création d'un site permettant de créer plus d'engagement sur un stream Twitch pour PierreShow."
competences: [c3, c4, c5]
---

## Contexte

Étant un ami proche de PierreShow et passant fréquemment sur ses streams Twitch, j'ai toujours voulu plus d'interactions entre le streamer et sa communauté.
Il avait un écran en rab qu'il allumait et plaçait derrière lui de façon à ce que l'écran soit visible, écran sur lequel il mettait des petites vidéos pour combler le vide.
Un jour il m'a proposé le projet de pouvoir permettre aux viewers de contrôler cet écran et de pouvoir y mettre n'importe quelle image (sous réserve que l'image respecte des règles bien fixes).

## Conditions et moyens

Le projet devait commencer en équipe mais tout le monde a vite oublié tout ça, j'ai donc repris le projet seul, mais avec des designs déjà définis pendant la phase en équipe.
Le projet a été fait sous forme de site web en html css js php avec quelques petits serveurs Node.js alentours pour gérer plusieurs flux d'images.

## Description de l'activité

1. On a premièrement défini en équipe ce que le site devait proposer et à quoi il ressemblerait.
2. Ensuite, j'ai commencé par créer le service qui permettrait d'afficher des images sur une page et qu'on puisse modifier l'image affichée sur cette page sans avoir à la recharger (service en socket).
3. Après ça, il a fallu créer l'interface permettant de modifier les images affichées depuis le site et non depuis des commandes brutes. Tout ça se fait depuis un système de file d'attente.
4. Ensuite, Il ne manquait plus que le fait d'ajouter des images dans la base de données du site
5. La fonctionnalité précédente étant trop dangereuse, il a fallu créer un système de modération.
(Chaque image uploadée n'est visible que par une équipe de modérateurs, ils doivent accepter cette image avant qu'elle puisse être visible sur le site et sur la page chargée par PierreShow pendant ses streams)

## Productions et preuves

![Modèle n°1 -- page Login, page Direct, et page Informations]({{ "/images/Modèle 1 -- Rubio.png" | relative_url }})
![Modèle n°2 -- page Images et page Liste]({{ "/images/Modèle 2 -- Rubio.png" | relative_url }})

## Ce que j'en retiens

J'étais tombé dans le piège de l'ia, mes pages commençaient à être lourdes et peu optimisées.
J'ai tout relu et remarqué que pour la page principale (page Images), l'ia avait fait en sorte de fare 50 requêtes en base de données au lieu d'une seule aggrégée, ce qui forçait la page à prendre ~2secondes à charger.
Une fois le problème réglé, la page ne mettait déjà plus que 200ms à charger.

Les pages ne sont toujours pas parfaitement optimisées mais font le boulot, je prévois de faire une version 2 de ce site.

Ce projet m'a permis d'apprendre le PHP (simples pages PHP sans fonctionnement complexe) et MongoDb.
Pour la deuxième version, grâce aux connaissances que j'ai acquises je pourrai avoir une structure beaucoup plus stable, sécurisée et rapide.
Exemple: la barre de navigation est hardcodée dans chaque page du projet n°1 alors que dans ce que j'ai du projet n°2, elle est séparée, écrite une seule fois et "invoquée" dans toutes les autres pages, ce qui fait que si je rajoute ou retire une page, je n'aurais à faire la modification qu'une seule fois.
Pareil, les appels en base de donnée ne sont plus fait par page, il y a toute une class PHP séparée qui gère ça.