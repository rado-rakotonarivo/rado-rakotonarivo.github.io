---
layout: post
title:  Premiers pas en Python
categories: teaching ip1-python
---

Commençons par le commencement, avant de nous lancer dans l'écriture d'un code voyons ce que c'est qu'un programme.

## Qu'est ce qu'un programme
Un **programme** est une suite d'instructions à exécuter par la machine et qui a pour but d'effectuer une tâche ou de résoudre un problème. Ainsi faire de la programmation signifie écrire des programmes.
Pour écrire des programmes il nous faut donc un langage qui soit à la fois compréhensible par le programmeur et la machine.

## Langage de programmation
* Un langage artificel et formel constitué d'un ensemble de règles (il n'y a pas d'ambiguïté dans un tel langage)
* Il est défini par une syntaxe/grammaire qui définissent qu'est ce qu'on peut écrire et qu'est ce qu'on ne peut pas écrire

## Transformer son code en exécutable
* Certains langages préfèrent transformer le code en fichier binaire afin d'être exécuter (compilé, qui passent par un compilateur: `C/C++`, `GO`, `Rust`)
* D'autres utilisent un interpréteur pour traduire et executer le code source (`haskell`, `scala`, `python`)

> A part le fait d'avoir un large choix de langage, il existe également une diversité dans l'approche de la résolution des problèmes: paradigme (impérative, fonctionnelle, orientée objet)

## Initiation à la programmation
Ce cours aura pour but d'apprendre à résoudre des problèmes en utilisant des programmes écrits en python :)
Nous ferons de la programmation impérative.

## Objectifs
Il sera question d'une vue d'ensemble sur les constructions du langage (identifier et donner un sens aux différentes constructions du langages):
 -- variables
 -- affectation
 -- boucle for
 -- instructions conditionnelles
 -- procédures et fonctions.

## Expression vs instruction

**expression** : décrit un calcul à faire/à évaluer par la machine.


**instruction** : décrit une action à faire par la machine.

1. Expression arithmétique:

* les expressions sont classifiées à l'aide de type correspondant à la forme des valeurs qu'elles calculent.

```
  type(exp) ---> renvoie le type de l'expression exp
```

* il existe plusieurs type de valeurs: `int, float, str, bool...`

* expression arithmétique
(a) constante entière
(b) variable
(c) deux expressions séparées par un opérateur arithmétique binaire
(d) une expression entourée de parenthèses
(e) une expression précédée du signe (-)
(f) appel de fonctions

* le type `int` contient tous les entiers représentables dans la limite de la mémoire de l'ordinateur (32 ou 64 bits)

```
0 --> 0 (1 bit) 000000000000000000000000000000000
1 --> 1 (1 bit) 000000000000000000000000000000001
4 --> 100 (4 bits) 000000000000000000000000000000100
```

> combien d'entiers positifs je peux représenter sur n bits? : $$2^n - 1$$.

* priorité opératoire

**associativité** permet de regrouper les termes sans changer le résultat: `(a + b) + c = a + (b + c)`

**division entière** `//` (renvoie `q`)
**modulo** `%` (renvoie `r`)


`a // b <=> a = b * q + r tel que 0 <= r < b (entiers naturels)`


```
  31 // 7 ---> 31 = 7 * 4 + 3
  a // b ---> a = b * q + r tel que:  (entiers relatifs)
  [pour b positif] --> 0 <= r < b
  [pour b négatif] --> 0 >= r > b
  -31 // 7 --> -31 = 7 * (-5) + 4
```

[Pour comprendre le détail de la méthode de calcul](http://python-history.blogspot.com/2010/08/why-pythons-integer-division-floors.html).

2. Variables:
* une variable associe un nom (identificateur) à une zone mémoire
* contient une valeur (contenu)
* créée par une affectation
* **affectation**: instruction qui permet de stocker/modifier la valeur d'une variable. (`=`) est le signe d'affectation (`<-`) se fait de la droite vers la gauche

```
variable <- expression
```

* la valeur d'une variable est amenée à être modifiée/changée au cours de l'exécution d'un programme. Les variables n'existent pas toutes au même moment (TRACE)

3- Controle de flux
* On fait de la programmation séquentielle ==> les instructions sont éxecutées les unes à la suite des autres
* l'execution du code se fait de haut en bas
* bloc de code == un ensemble d'instructions
* controler le flux == modifier le flux d'execution
  + conditionnelle (choisir d'executer ou non un bloc)
  + boucle (répéter un bloc)

(a) instruction conditionnelle (if else)
```
if (condition):
  | bloc
else:
  | bloc
```
la condition est une expression booléenne (a comme valeur vrai ou faux) **permet de sauter des blocs de code**.

> La règle pour faire évoluer la mémoire sur une conditionnelle est la suivante : si la ligne PC+1 est une conditionnelle, on évalue d’abord la condition : si elle est vrai on exécute la ligne PC+2, sinon on exécute la ligne qui suit le else. Si la ligne PC+1 est un else (donc on a terminé l’exécuter le bloc associé à un if), on exécute la ligne après le bloc associé au else. Ces règles seront décrites plus en détail dans les prochaines chapitres, dans cette première présentation, il faut juste donner l’intuition que la conditionnelle nous permet de sauter des lignes de code.

(b) boucle bornée (for)
* on connait à l'avance le nombre de fois où l'on veut répéter le code
```
for i in range(start, stop, step):
  | bloc
i ==> compteur de boucle (accessible hors de la boucle)
start ==> première valeur de i
stop ==> valeur de sortie de la boucle
step ==> incrémentation de i
```
Par exemple:

```
for i in range(0, 3, 1):
i = {0, 1, 2}

for i in range(0, 3, 2):
i = {0, 2}
---------------------------
1 x = 0
2 for i in range(0, 3, 1):
3 |   x = x + i
4 z = x
---------------------------
PC | x | i | z
1  | 0 |   |
2  | 0 | 0 |
3  | 0 | 0 |
2  | 0 | 1 |
3  | 1 | 1 |
2  | 1 | 2 |
3  | 3 | 2 |
4  | 3 | 2 | 3
```

4- fonctions/procédure
* une **fonction** sert à nommer un calcul dont le résultat et renvoyé par l'instruction `return`
* la définition d'une fonction correspond à décrire le calcul effectué par la fonction
* l'appel d'une fonction signifie utiliser la fonction avec les paramètres données en entrée

```
def nom_fonction([parametres]):
  | bloc
  | return <valeur_de_retour>
```

* **procédure** nomme une suite d'instructions sans renvoyer de résultat

> appel de fonction ==> expression / appel de procédure ==> instruction

```
def nom_procedure([parametres])
 | bloc
 | (return None)
```

Cheat sheet:
===========
1 - Entrée/Sortie (input/output): interaction avec le programme
-> entrée: donner une entrée au programme (le périphérique d'entrée standard est le clavier)
-> sortie: recevoir une réponse du programme (le périphérique de sortie standard est l'écran ~~~ la console)

* Les fonctions/commandes qui nous permette de les utiliser:

entrée:
--
x = input(prompt)

  -> prompt est la chaîne de caractère affichée dans la sortie standard
  -> affecte dans la variable x la valeur (chaîne de caractère) entrée au clavier
  /!\ pour lire un autre type depuis l'entrée standard il faudra faire un cast de la valeur lue:
      cast == transformer un type en un autre
--
# lire un entier du clavier
n = int(input("Saisir un entier: "))

sortie:
--
print(object(s), sep=separateur, end=caractere_de_fin, file=file, flush=flush)

-> on peut afficher autant d'objets/variables que l'on souhaite (à séparer par une virgule)
--
x = 10
y = "salut"
print(x, y) ---> 10 salut
-> sep spécifie le séparateur des variables que l'on veut afficher (par défaut c'est un espace ' ')
-> end spécifie le caractère à afficher à la fin de l'affichage (par défaut c'est le caractère de saut de ligne '\n')
--
print("hello", "world", end="!\n") ---> hello world!

-> écriture formatée
print("%format texte" % (variable))
