---
title: "🇫🇷 Les string interné avec 🐍"
subtitle: ""
date: 2020-06-23
draft: false
---

En python les string sont immutables. Plusieurs variables peuvent référencer le même string pour économiser de la mémoire et éviter de créer un nouvel objet à chaque fois.

Avec l'implémentation CPython, python va créer des `interned` string de manière implicite.

* un string est interné si sa taille vaut 0 ou 1
* un string est interné uniquement à la compilation (`abc` sera interné mais pas `''.join(['a', 'b', 'c'])`)
* un string interné doit être composé uniquement de lettres ASCII, de chiffre, ou du caractère `_`.
* un string interné ne doit pas avoir plus de 20 caractères

## Ressources

* http://foobarnbaz.com/2012/07/08/understanding-python-variables/
* https://medium.com/@bdov_/https-medium-com-bdov-python-objects-part-iii-string-interning-625d3c7319de
* http://guilload.com/python-string-interning/
* https://stackoverflow.com/questions/15541404/python-string-interning
* https://www.codementor.io/@satwikkansal/do-you-really-think-you-know-strings-in-python-fnxh8mtha
* https://stackoverflow.com/questions/17679861/does-python-intern-strings