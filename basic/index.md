# Atelier Python : Introduction de base

---

# INTRODUCTION

* Objectifs
    * **explorer Python** par l'expérimentation et l'introspection dans l'interpréteur
    * **maîtriser les notions de base** : types, fonctions, conditionnels, itérations...
    * **écrire un script** qu'on exécutera dans l'interpréteur
    * **importer** la puissance de Python

* Documentation
    * [Documentation officielle][python-doc]
    * [Tutoriel officiel][python-tutorial]
    * [Standard Library][python-library]
    * [Python for Data analysis][data-analysis]
      * Chapitre 1 : pour *Pourquoi Python*
      * Chapitre 3 : pour *IPython avancé*
      * Chapitre 6 : pour *Manipulation texte, CSV, JSON, HTMl, XML et .xls*
      * Annexe : pour *Python*
    * Modules
      * [PyPI][pypi]
      * [Pythonpedia][pythonpedia]

* Environnement
    * éditeur texte : gedit, vi/vim, emacs, nano, atom...
    * interpréteur Python : python, ipython

* [Setup technique][setup]

----

# I. THÉORIE (quoi)

## Programmer

* données
    * typées, structurées en variables
* operations sur données
    * fonctions transforment données d'input en données d'output
    * stocker, récupérer de fichiers, bases de données, Internet
* langages formels
    * syntaxe
* orienté objet
    * modéliser le monde
    * regrouper à un endroit la définition des sortes de choses dans le monde
    * regrouper à un endroit les variables et fonctions pertinentes aux *objets* de même *classe*

Schéma : [Orienté-objet][schema-oo]

## Python

* interprété
* orienté-objet
* dynamique
* fortement typé
* ... utilisé (presque) partout

* Python 2 vs Python 3
* Python Anaconda
* interpréteur : Python (vanille) vs IPython (interactif, introspection)
        $ python
        $ ipython

## Programmer en Python

Schéma : [Programmer en Python][schema-programmer]

### Environnement

* Wes McKinney, *[Python for Data analysis][data-analysis]*, O'Reilly, 2013, p.11
* ... à propos des Integrated Development Environments (IDEs), ex.: PyCharm

    > *When asked about my standard development environment, I almost always say "IPython plus a text editor". I typically write a program and iteratively test and debug each piece of it in IPython. It is also useful to be able to play around with data interactively and visually verify that a particular set of data manipulations are doing the right thing. Libraries like pandas and NumPy are designed to be easy-to-use in the shell.*

### Approche

1. Explorer dans l'interpréteur interactif IPython
2. Écrire dans son script ce qui fonctionne
3. Chercher les outils qu'il vous faut (documentation, pypi, Internet, communauté, livres...)
4. Importer (pourrait être nécessaire d'installer d'abord) ces outils et  
construire des scripts plus complexes, des programmes
5. Créer ses modules ou programmes
6. Les partager et collaborativement créer de meilleurs outils

### Syntaxe

* commentaires: `#`
* variables: sans `$`
* énoncés: sans `;`
* block: sans `{}`
* continuer sur autre ligne: `\` ou parenthèses
* style: [PEP 8][pep8]
    * flake8 pour vérifier la conformité

            $ sudo pip install flake8
            $ flake8 filename.py

---

# II. DÉMO (comment)

## Explorer

* données dans les variables de base : `nom`, `prenom`, `date_naissance`, `est_fournisseur`,
* les transformer avec des fonctions : `age()`
* ... ou des méthodes (fonctions sur objets) : `nom.upper()`

## Coder un script

* créer une structure de données complexe : une classe `Personne`
* interagir avec l'utilisateur
* sauvegarder les données dans un fichier

## Importer la puissance de Python

* aller plus loin grâce aux outils exitants
    * importer de la standard library (venant avec Python) : `datetime`

---

# III. PRATIQUE (hands-on : faites-le)

## Environnement

* créer un répertoire `atelier`

        ~$ mkdir atelier

* s'y déplacer

        ~$ cd atelier
        ~/atelier$

* lancer l'interpréteur

        ~/atelier$ ipython

## Variables

### Nom, valeur, référence

* les noms de variables font référence à des valeurs

        a = 12
        b = a
        id(a)
        id(b)

* plusieurs noms peuvent faire référence à la même valeur
* l'assignation à un nom de variable n'affecte pas les autres variables

        a = 12
        b = a
        a = 6
        print a, id(a)
        print b, id(b)
* l'assignation ne copie pas de données
* un changement à une valeur est visible par toutes les variables qui y font référence

        a = [1, 2, 3]
        b = a
        a.append(4)
        print b         # [1, 2, 3, 4]
        a = a + [5]     # on assigne une nouvelle valeur, [1, 2, 3, 4] + [5], à a
        print b         # [1, 2, 3, 4]

* les valeurs sont effacées lorsqu'aucune variable n'y fait référence
* on ne peut pas effacer une valeur nous-même, seulement une variable

* Voir http://nedbatchelder.com/text/names.html pour une longue explication très détaillée

### Types

* typage dynamique (pas besoin de le déclarer)

        n = None        # NoneType : type spécial voulant dire... rien
        b = True        # bool : booléen... True ou False n'oubliez pas les majuscules

        i = 15          # int: entier
        f = 15.5        # float: décimal

        s = "string"    # str: chaine de caractère, instancié avec "" ou ''
        u = u"string"   # unicode: chaîne de caractère unicode, instancié avec u"" ou u''

        l = []          # list: liste d'objets (ordonné)
        t = ()          # tuple: liste immuable d'objets
        d = {}          # dict: dictionnaire de données (unique, non-ordonné), clés-valeurs
        d = {'a': 1, 'b': 2}

        st = set()      # set: ensemble (unique, non-ordonné), set([])
        st = {1, 2, 3}

* dépaqueter

        coord_mtl = (45.30, 73.34)
        lat, lon = coord_mtl

* fortement typé (sans transtypage explicite)
* transtypage:  
`str()`, `int()`, `float()`, `bool()`, `list()`, `tuple()`, `dict()`, `set()`

        float(12)

### Conteneurs

* imbrication

        l = [[1,2,3],[4,'hey!',6],[7,8,9]]
        d = {1611: {'nom':u'Baragiotta', 'prenom':u'Davin'},
             123: {'nom':u'Leduc-Hamel', 'prenom':u'Mathieu'}}

* indexing

        l[2]
        d[1611]
        l[1][1]

* slicing

        l[1:3]

### Exercice : variables

1. créer une liste de produits, un catalogue
1. créer un dictionnaire représentant une personne, avec ces données :
    * nom
    * prenom
    * sexe (ou genre)
    * année de naissance
    * est client ou pas
    * sa liste de souhaits de produits (à partir du catalogue)

## Fonctions

### Appel de fonction

* nom de fonction : `open`
* appel de fonction : `open()`

### Fonctions built-in

* Documentation officielle : [Fonctions built-in][python-functions]

        type()                    # retourne le type de l'objet
        dir()                     # retourne les noms derrières l'objet
        help()                    # retourne l'aide
        callable()                # dit si un objet est appelable, exécutable...

        bool(), int(), str()      # initialisation ou transtypage (conversion)
        getattr()
        hasattr()

        isinstance(object, Type)  # teste la classe (ou type) d'un objet
        issubclass()
        super()

        len()
        min()
        max()

        open()
        range()
        raw_input()

        enumerate()
        zip()
        sorted()
        reversed()

        print
        del

### Déclarer une fonction

* convention de nommage
* output : `None` par défaut, une ou plusieurs valeurs
* input : paramètres positionnels ou nommées
* portée des variables
* `*args`, `**kwargs`

        def ma_fonction(param1, param2, param3=None, param4=0, \*args, \*\*kwargs):
            """Ceci est ma fonction."""
            output = True
            return output

### Exercice : fonctions

1. créer une fonction qui retourne l'âge de quelqu'un en fonction de sa date de naissance.

## Namespaces

### Objets

* objet : tout est un objet
* attribut = variable sur un objet
* méthode = fonction sur un objet

        objet.attribut
        objet.methode()
        objet.attribute.methode()
        objet.methode().attribut
        objet.attribut.attribut
        objet.methode().methode()

### Introspection

* variable. [+ tab]
* variable?

* `type()`
* `dir()`
* `help()`

* exploration des types

### Exercice : namespaces

1. ajouter un produit au catalogue des produits
1. compter le total des produits que vous avez dans votre catalogue
1. créer le nom complet (à partir du nom et du prénom) de votre personne mais avec son nom en majusucule
1. ajouter sur le dictionnaire d'une personne, une nouvelle clé pour ses achats

        nom = u"Davin Baragiotta"
        prenom, nom = nom.split()
        nom.upper()
        nom.lower()
        nom.ljust(30)
        nom = [prenom.lower(), nom.lower()]
        username = ".".join(nom)

        nom = u"Davin Baragiotta"
        username = ".".join(nom.split()).lower()

        users = []
        users.append(username)

        davin = {'prenom':u'Davin', 'nom':u'Baragiotta'}
        max = {'prenom':u'Maxime', 'nom':u'Chambreuil'}
        piero = {'prenom':u'Pierre', 'nom':u'Lamarche'}
        marco = {'prenom':u'Marc', 'nom':u'Cassuto'}

        personnes = []
        personnes.append(davin)
        personnes.append(max)
        personnes.append(piero)
        personnes.append(marco)

        status = [
            (1, u'Draft'),
            (2, u'In progress'),
            (3, u'Rejected'),
            (4, u'Accepted'),
        ]

## Flux et contrôle

### Comparaison et opérateurs

* faux = `False`, `0`, `""`, `()`, `[]`, `{}`, `None`
* `and`, `or`, `not`
* `< > <= >= == !=`
* `x < y <= z`
* `is`, `is not`
* `in`, `not in`

### Conditionnel

* `if`, `elif`, `else`

        numlist = range(6)
        if 5 in numlist:
            print 'hourra 5'
        elif 4 in numlist:
            print 'hourra 4'
        else:
            print 'pas hourra :-('

* one-liner

        'hourra 5' if 5 in numlist else 'pas hourra :-('

### Itération

* `while`

        annee = 2012
        while annee <= 2015:
            print annee
            annee = annee + 1   # annee += 1

* `for`

        for i in range(2012, 2016):
            print i

### Exercice : flux et contrôle

1. écrire un test pour vérifier si un produit est dans la liste de souhaits de la personne
    * si oui, l'ajouter dans ses achats
        * ce serait pas mal d'avoir une date associée à l'achat
    * si non, lui donner des arguments pour acheter ce produit (imprimer à l'écran)
1. de tous les produits dans la liste de souhaits, lister seulement ceux qui n'ont pas été achetés encore

## Scripts

* exemple de script: [coucou.py][coucou]

        #! /usr/bin/env python
        # -*- encoding: utf-8 -*-

        def coucou(nom):
            return u"Coucou %s!" % (nom,)

        if __name__ == '__main__':
            print u"--------------------------------------------------"
            print u"DÉBUT du script"
            print u"--------------------------------------------------"
            nom = raw_input("Quel est votre nom? ")
            print coucou(nom)
            print u"-----------------------------------------------"
            print u"FIN du script"
            print u"-------------------------------------------------"

* shebang: `#!/usr/bin/env python`
* encoding: `# -*- encoding: utf-8 -*-`
* `if __name__ == '__main__':`
* `raw_input()`

* exécution dans IPython:

        %run script.py
        run script.py

* exécution dans Python:

        $ python script.py

### Exercice : scripts

1. créer un fichier appelé `script.py`
1. ajouter le code testé dans l'interpréteur qui fonctionne
    * variable pour le catalogue de produits
    * fonction pour calculer l'âge
1. demander à l'utilisateur toutes les questions nécessaires pour obtenir ses données personnelles à mettre dans son dictionnaire
1. terminer l'interaction avec l'utilisateur avec un commentaire pertinent relatif à son âge et les produits dans sa liste de souhaits
1. exécuter votre script
1. interagir avec votre script
1. fermer l'interpréteur
1. ré-exécuter le script

## Classes

### Déclarer une classe

        class Personne(object):

            def __init__(self, nom, prenom, date_naissance=None):
                self.nom = nom
                self.prenom = prenom
                self.date_naissance = date_naissance

            def age(self):
                # TODO : calculer à partir de date_naissance et date d'auj.
                return 2015 - self.date_naissance

### Créer des objets

* objets, instances d'une classe

        piero = Personne("Pierre", "Lamarche")
        marco = Personne(prenom="Marc", nom="Cassuto")
        bruno = Personne(nom="Joliveau", prenom="Bruno")

### Exercice : classes

1. écrire une classe `Personne` dans un autre script nommé `models.py`
1. exécuter le script `models.py`
1. créer quelques objets personnes (instances) à partir de votre classe `Personne`
1. quand tout est à votre goût, remplacer dans le premier script (`script.py`) le dictionnaire de personne et la fonction `age` avec votre classe `Personne`

## Importer

Schéma : [Import][schema-import]

        import module
        import module as my_module
        from module import name
        from module import name as my_name
        from module import name, name2, name3

* built-in : pas besoin d'import
* standard library (shipped with Python): import sans installation
* pypi : plein de modules à installer qui n'attendent qu'à être importés
    * [http://pypi.python.org][pypi]
    * installation avec pip

* importable si installé dans le path
* ordre des imports selon [PEP 8][pep8] : du général au particulier

### Modules de la Standard Library

* Documentation officielle : [Standard Library][python-library]

        from datetime import date

        auj = date.today()
        print auj
        #année = ??

        import sys
        sys.path

#### Exemples

* re
* datetime
* collections
* pprint
* decimal
* os.path
* pickle
* sqlite3
* zipfile
* csv
* email
* json
* htmllib
* urllib2
* Tkinter, ttk
* pdb
* sys

#### Exercice : importer de la standard library

1. importer le nom `date` du module `datetime` de la standard library
1. créer la date d'aujourd'hui
1. explorer comment obtenir l'année à partir d'une date
1. upgrader votre méthode calculant l'âge sur la classe `Personne` pour que le calcul se fasse à partir de dates et non d'entiers
1. explorer comment gérer les jours pour le calcul de l'âge (vous n'avez pas le même âge dans une même année si votre anniversaire est à venir ou déjà passé)
1. upgrader encore votre méthode `age` pour utiliser les deltas de date

### Vos propres modules

        __init__.py
        __name__
        __main__

* `__name__` : Nom du module.   
C'est le nom de fichier si importé, mais c'est `__main__` si exécuté (utile pour les tests)
* ajouter un fichier `__init__.py` (vide) dans un répertoire pour en faire un module Python

#### Exercice : importer votre module

1. créer un répertoire nommé `ecommerce` sous le répertoire `atelier`
1. créer un fichier `__init__.py` dedans
1. déplacer votre fichier `models.py` dedans
1. dans l'interpréteur, importer la classe `Personne` vivant dans `models.py` afin de la tester
    * s'assurer que le répertoire `ecommerce` est "dans le path" de l'interpréteur
    * lancer l'interpréteur dans le répertoire parent immédiat rend votre module "dans le path", accessible à l'interpréteur

### Modules tiers

* pypi = [python packaging index][pypi]
* les modules qu'on importe vivent dans des paquets à installer sur notre système
* identifier le paquet pertinent (sur pypi ou en parlant avec des Pythoneux)

#### Bases de données

* DB : sqlite3, mysqldb, psycopg2
* ORM : sqlalchemy

#### Développement web

* django (+south)
* pyramid
* flask

#### Science

* numpy
* matplotlib
* pandas
* scipy

##### Psychologie

* psychopy

#### Administration système

* fabric
* celery
* ansible
* ...

#### Traitement des langues naturelles

* nltk
* pattern

#### Installation avec pip

* pip = pip installs Python
* pip installe les paquets sur votre machine
* pour une meilleure gestion des paquets, utiliser virtualenv (couvert dans un autre atelier)

        $ sudo pip install packagename

### Exercice : importer un module tiers

1. installer `feedparser` sur votre machine (virtuelle)
    1. fermer l'interpréteur (ou ouvrir un nouveau terminal)
    1. installer avec pip
    1. relancer l'interpréteur
1. importer `feedparser`
1. explorer `feedparser`

## Fichiers

* ouvrir, manipuler, fermer
    * exemple de fichier : [texte.txt][texte]

              f = open('texte.txt')
              for line in f.readlines():
                  print line,
              f.close()

              f = open("texte.txt")
              lines = f.readlines()
              f.close()

              with open('texte.txt') as f:
                 for line in f:
                     print line

              target = 'python'
              context = [line for line in lines if target in line]
              comments = [line for line in lines if line.startswith('#')]

### Exercice : fichiers

1. introspecter la fonction `open` pour voir comment  
ouvrir en écriture, lecture, ajout en fin de fichier... : r, w, a...
1. créer une liste de strings
1. écrire ces strings dans un fichier, ex.: `test.txt`

## Plaisirs syntaxiques

### Compréhension de listes, dictionnaires et ensembles

* créer une liste, un dictionnaire ou un ensemble à partir d'un itérable avec un "one-liner"

        new_list = [v for v in old_list if v < 2]
        new_dict = {k, v for k, v in old_dict.items() if k < 2}
        new_set = {v for v in old_list if v < 2}

* équivalent à une boucle

        new_list = []
        for v in old_list:
            if v < 2:
                new_list.append(v)


### Formatage de chaînes

* substitution : `%`

        for n in range(10):
            print "La puissance 3 de %d est : %d" % (n, n**3)

        for p in people:
            print "Bonjour %s %s" % (p['prenom'], p['nom'].upper())

* formattage: str.format

        for n in range(10):
            print "La puissance 3 de {0} est {1}".format(n, n**3)

### Exercice : formatage de chaînes

1. utiliser le formatage de chaînes pour les questions posées ou les réponses données à l'utilisateur (ex.: âge)

## Exceptions

* try, except

        try:
            15/0
        except (ZeroDivisionError,), e:
            print "Diviser par zéro c'est mal, vous voyez?"
            print e

### Exercice : exception

1. dans votre méthode `age`, retourner un message d'erreur explicite lorsque l'input n'est pas une date

## Debug

* break point
* introspection
* les enlever après debug, ahem...

        import pdb; pdb.set_trace()

## Tests

* unittest
* doctest
* tests fonctionnels
  * Suivi [chez SFL][sfl-test]

## Permanence des données

* fichiers
* sérialisation : `import pickle`

        import pickle

        f = open('pickles', 'w')
        pickle.dump(status, f)
        pickle.dump(people, f)
        f.close()

        exit()

        import pickle

        f = open('pickles')
        pickle.load(f)
        #objects = []
        #for obj in pickle.load(f):
        #    objects.append(obj)
        f.close()

* en base de données?

### Exercice : permanence des données

1. dans votre fichier `script.py`, stocker toutes les réponses obtenues de l'utilisateur dans un fichier .csv
    1. importer le module csv de la standard library
    1. explorer comment écrire un fichier csv avec le module csv... csv.writer?
    1. s'assurer que le programme écrive dans le fichier en mode append afin de ne pas perdre de données à chaque utilisation
1. tester plusieurs fois votre programme, vérifier que le .csv accumule les données

# CONCLUSION

## Aller plus loin

* Conférences
    * [PyCon], [PyCon.ca]
    * [SciPy]
* Videos
    * [PyVideo]
* Data analysis
    * [pydata], [pandas]
    * Wes McKinney, *[Python for Data analysis][data-analysis])*, O'Reilly, 2013

## Ce que on a appris

* `import antigravity`
* documentation + interactivité + introspection
* scripts + modules + import

## Obtenir de l'aide

* communauté pour aider
* [Montréal-Python][mtlpy]:
    * entrer dans la communauté

* enjoy!

# EXERCISE

## Objectif

Créer un script `flux.py` dans le répertoire `atelier/actus` qui retournera les 5 dernières actualités affichées sur le site de Montréal-Python
[http://montrealpython.org/fr/feed/][mtlpy-feed]

## Approche

1. utiliser feedparser
        $ sudo pip install feedparser

1. lancer interpréteur et suivre exemple de la doc :
    * ipython
    * http://packages.python.org/feedparser/
1. introspecter (et imprimer dictionnaire pour voir ses clés) au besoin
1. coder le script qui fera le traitement voulu
1. lancer le script dans l'interpréteur pour confirmer son exécution correcte
1. servir froid

## Algorithme

* capter le flux RSS de http://montrealpython.org
* retenir le nombre d'items voulu
* traiter les items retenus :
    * créer une chaîne de caractères unique : avec les infos des derniers items modifiés (titre, URL... et éventuellement la date de dernière modification)

## Solution

Prenez le temps de coder vous-même une solution...  
... ensuite vous pouvez comparer avec : le [solutionnaire]

Pour info, notre solution ne fait que 8 lignes Python.

---

[setup]: setup.md
[coucou]: coucou.py
[texte]: texte.txt
[solutionnaire]: solutionnaire.md

[schema-programmer]: schema-programmer.jpg
[schema-oo]: schema-oo.jpg
[schema-import]: schema-import.jpg

[python-doc]: http://www.python.org/doc/
[python-tutorial]: http://docs.python.org/tutorial/
[python-library]: http://docs.python.org/library/
[python-functions]: http://docs.python.org/2/library/functions.html

[pep8]: http://www.python.org/dev/peps/pep-0008/
[pypi]: http://pypi.python.org
[data-analysis]: http://shop.oreilly.com/product/0636920023784.do
[pythonpedia]: https://pythonpedia.com/

[sfl-test]: http://test.savoirfairelinux.com/

[PyCon]: http://pycon.us
[PyCon.ca]: http://pycon.ca
[SciPy]: http://scipy.org
[PyVideo]: http://pyvideo.org
[pydata]: http://pydata.org
[pandas]: http://pandas.pydata.org

[mtlpy]: http://montrealpython.org/
[mtlpy-feed]: http://montrealpython.org/fr/feed/
