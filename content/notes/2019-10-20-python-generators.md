---
title: "🇫🇷 Les générateurs avec Python"
subtitle: ""
date: 2019-10-20
draft: false
---

## Définition

* Un __générateur__ est un *itérateur* mais un itérateur n'est pas un générateur
* Un itérateur est n'importe quel objet qui possède les méthodes `__next__`, `__iter__` et qui retourne `self`
* Un générateur
    + possède au moins une ou plusieurs instructions `yield`
    + peut également utiliser l'instruction `return`
    + permet de garder une trace de l'état interne de la fonction
    + doit lever l'exception `StopIteration` quand il n'y a plus de valeurs à retourner
    + retourne un itérateur, mais son exécution ne commence pas immédiatement
* L'instruction `yield` :
    + met en pause la fonction
    + les variables locales et leurs états sont sauvées et accessibles lors des prochains appels
    + donne la main à la fonction appelante
* L'instruction `return` termine complètement une fonction

## Cas d'usage

* Lire le contenu de fichiers très volumineux
* Boucler sur une liste inifinie

## Ressources

https://realpython.com/introduction-to-python-generators/#using-generators
