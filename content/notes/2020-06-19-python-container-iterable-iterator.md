---
title: "🇫🇷 Les conteneurs avec 🐍"
subtitle: ""
date: 2020-06-19
draft: false
---

# Itérable

Un objet sur lequel on peut itérer, capable de renvoyer ses éléments un à un.

* Objet de type séquence : `list`, `str`, `tuple`, ...
* Objet de type mapping : `dict`, ...
* Classse ayant une méthode `__iter__()` ou `__get_item__()`

> Lorsqu'un itérable est passé comme argument à la fonction native `iter()`, celle-ci fournit en retour un itérateur sur cet itérable.

```python
>>> l = [1, 2, 3]
>>> from collections.abc import Iterable
>>> isinstance(l, Iterable)
True
>>> iterator = iter(l)
>>> iterator
<list_iterator object at 0x1091aa110>
```

# Itérateur


Objet qui représente un flux de données, il doit implémenter les méthodes suivantes :

* `__iter__()` : retourne l'objet itérateur lui même (chaque itérateur est donc un itérable)
* `__next__()` : retourne successivement les objets du flux
    * lève l'exception `StopIteration` lorsque plus aucune donnée n'est disponible

```python
>>> l = [1, 2, 3]
>>> iterator = iter(l)
>>> next(iterator)
1
>>> next(iterator)
2
>>> next(iterator)
3
>>> next(iterator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

> Un objet conteneur, (tel que `list`) produit un nouvel itérateur neuf à chaque fois qu'il est passé à la fonction `iter()` ou s'il est utilisé dans une boucle for. Faire ceci sur un itérateur donnerait simplement le même objet itérateur épuisé utilisé dans son itération précédente, le faisant ressembler à un conteneur vide.

```python
>>> l = [1, 2, 3]
>>> iter(l)
<list_iterator object at 0x1091aa110>
>>> iter(l)
<list_iterator object at 0x1091aa050>
```

# Conteneur

Objet ayant pour vocation à contenir d'autres objets (`str`, `list`, `tuple`, `dict`, ...).

Doit définir la méthode `__contains__()`, afin d'utiliser l'opérateur `in`.

```python
>>> 'a' in 'abc'
True
>>> 'abc'.__contains__('a')
True
```

Il existe deux type de conteneurs :
* **subscriptable** (`str`, `list`, `tuple`, `dict`, ...)
* non **subscriptable** (`set`, `frozenset`, ...)

Un conteneur dit *subscriptable* concerne tous les objets sur lesquels l'opérateur `[]` peut être utilisé, c'est à dire n'importe quel objet qui implémente la méthode `__getitem__()`.

```python
a[1]
# pareil que
a.__getitem__(1)
```

2 catégories de *subscriptables* (non exclusif) :
* les **indexables** : peut être indexé avec des nombres entiers
* les **sliceables** : peut être indexé avec des `slice`

## Séquence

Une séquence est un conteneur qui est *indexables* et *sliceables*.

* Itérable qui supporte l'accès à un élément en utilisant un entier comme indice
* Itérable qui définit la méthode `__len__()` qui retourne la taille de la séquence

Ex : `str`, `list`, `tuple`, `range`, `binary data`, `dict` ([mais considéré comme un mapping](https://docs.python.org/3/glossary.html#term-sequence))

| Hérite de | Mét. abstraites | Méth. mixin |
| --------- | ------------------- | -------------- |
| `Reversible`, `Collection` | `__get_item__`, `__len__` | `__contains__`, `__iter__`, `__reversed__`, `index`, `count`|

## Mapping

Un *mapping* est un conteneur qui associe des clefs à des valeurs.

| Hérite de | Mét. abstraites | Méth. mixin |
| --------- | ------------------- | -------------- |
| `Collection` | `__get_item__`, `__len__`, `__iter__` | `__contains__`, `keys`, `items`, `values`, `get`, `__eq__`, `__ne__` |


# Les objets indexeables

L'opérateur `[]` permet :

* d'accéder à un élément de l'objet (`__getitem__`)
* de modifier un élément si l'objet est mutable (`__setitem__`)
* de supprimer un élément si l'objet est mutable (`__delitem__`)

Dans la stdlib, les listes, les chaînes de caractères, les tuples et les dictionnaires sont indexables mais pas les sets.

# Les objets sliceable

Un sliceable est souvent indexable, mais l’inverse n’est pas forcément vrai. Dans la stdlib, les listes, les strings et les tuples sont sliceables, mais pas les dictionnaires ni les sets

# Ressources

* https://docs.python.org/fr/3/glossary.html#term-iterable
* https://docs.python.org/fr/3/glossary.html#term-iterator
* https://docs.python.org/3/library/collections.abc.html
* https://www.geeksforgeeks.org/python-difference-iterable-iterator/
* https://zestedesavoir.com/tutoriels/954/notions-de-python-avancees/1-starters/1-containers/