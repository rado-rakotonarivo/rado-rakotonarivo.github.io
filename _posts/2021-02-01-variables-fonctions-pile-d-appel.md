---
layout: post
title:  "Notes sur les variables et leur portée, pointeurs [Prog 2]"
categories: teaching prog-2
permalink: /posts/variables-pointeurs
---

<p>Vous trouverez les énoncés des TD sur le moodle du cours <a href="https://moodlelms.univ-paris13.fr/course/view.php?id=547">ici</a>.</p>

<h2 class="listing">Variables et Pointeurs</h2>

<span class="question"> Rappel : </span> une <code>variable</code> est une zone mémoire caractérisée par :

<ul class="tips">
  <li> un nom (permettant de l'identifier dans notre programme)</li>
  <li> un type (pour spécifier le nombre d'octet nécessaire pour encoder notre variable)</li>
  <li> une valeur (la donnée contenue à l'intérieur de notre variable) </li>
  <li> une adresse (l'endroit de la mémoire où est enregistrée notre variable) <b>[déterminée à l'execution]</b></li>
</ul>

Voyons ce qui se passe en mémoire quand on déclare et initialise la variable suivante.
{% highlight c %}
int x = 10;
{% endhighlight %}

- On déclare une variable qui sera identifié par le nom `x`.
- `x` est de type entier (`int`). Dans la mémoire, les entiers sont représentés sur 4 octets. La zone mémoire réservée pour `x` sera donc de 4 octets.
- On initialise `x` à 10, ie `x` a pour valeur initiale 10.
- Puis imaginons que `x` soit stockée à l'adresse 80 de la mémoire, ie son adresse est 80.

{% highlight plaintext %}
   x
--------
|  10  |
--------
   80
{% endhighlight %}

<span class="question"> Pointeur ? </span> un `pointeur` est une variable dont le contenu est l'adresse d'une autre variable (pour l'instant &#128521;). Puisqu'un `pointeur` est une variable il a donc toutes les caractéristiques d'une variable : nom, type, valeur et adresse.

{% highlight c %}
int x = 10;
int *px = &x;
{% endhighlight %}

- On déclare une variable nommée `px`.
- `px` est de type `int *`. Cela indique que la variable dont l'adresse est contenue dans `px` a pour type `int`.
- On initiale `px` à l'adresse de `x` notée `&x`. On dit que `px` pointe sur `x` et que `x` est pointé par `px`.
- Puis imaginons qu'à l'execution `px` soit stockée à l'adresse 102 dans la mémoire.

{% highlight plaintext %}
   x                px
--------         --------
|  10  |         |  80  | (80 est l'adresse de x)
--------         --------
   80               102
{% endhighlight %}

<p class="tips"> Le <code>type</code> du pointeur determine la taille de la tête de lecture. Quand on écrit <code>*px</code> cela signifie : va à l'adresse contenue dans <code>px</code> et lit <code>4 octets</code> à partir de cette adresse (car <code>px</code> est de type <code>int *</code>).</p>

On affiche le contenu d'un pointeur (une adresse) avec le format `"%p"`.

{% highlight c %}
int x = 10;
int *px = &x;
printf("L'adresse de x est : %p\n", &x);
printf("Le contenu de px est : %p\n", px);
{% endhighlight %}

Ce bout de code produit l'affichage suivant :

{%highlight plaintext%}
L'adresse de x est : 0x7ffeeedda838
Le contenu de px est : 0x7ffeeedda838  
{%endhighlight%}


<span class="question"> Mais à quoi ça sert ? </span> Un pointeur permet d'accéder (lire et écrire) à la valeur de la variable dont l'adresse est contenue dans le pointeur. Si `px` est de type `int *`, alors `*px` est de type `int`.

<br/>

Qu'affichera le programme suivant ?

{% highlight c linenos%}
#include <stdio.h>

int main () {
  int x = 10;
  int *px = &x;
  (*px) = (*px) + 1;
  printf("x vaut : %d\n", x);
  return 0;
}
{% endhighlight %}

Le programme affichera `x vaut : 11`. À la ligne 6, l'instruction `(*px) = (*px) + 1;` incrémente la valeur de la variable dont l'adresse est contenue dans `px` ie la valeur de `x`.

<br/>

On verra par la suite toutes les possibilités que l'on peut avoir avec les pointeurs. Cependant il faut faire attention à leur utilisation car on a vu qu'avec les pointeurs on a directement accès à la mémoire.

<h2 class="listing"> Fonctions </h2>

Le petit rappel sur les `fonctions` est disponible [ici](/posts/fonctions-menus)

<h2 class="listing"> Portée des variables </h2>

On rappelle qu'un bloc d'instructions est délimité par des accolades :`'{'` et `'}'`. En règle générale, la `portée d'une variable` est limitée dans le bloc dans lequel elle a été déclarée. C'est-à-dire qu'elle n'est accessible en lecture et en écriture qu'à l'intérieur du bloc dans lequel la variable a été déclarée.

Le code `demo_portee.c` suivant produit une erreur :

{%highlight c linenos%}
#include <stdio.h>

int main(int argc, char const *argv[]) {
  int a = 0;
  ++a;

  if (a == 1) {
    int b = 2;
    printf("a vaut : %d\n", a);
    printf("b (if) vaut : %d\n", b);
  }
  ++b;
  printf("b (main) vaut : %d\n", b)

  return 0;
}
{%endhighlight%}

En compilant on tombe sur l'erreur suivante :

{%highlight plaintext%}
$ gcc -Wall -o run demo_portee.c
demo_portee.c:12:5: error: use of undeclared identifier 'b'
  ++b;
    ^
demo_portee.c:13:34: error: use of undeclared identifier 'b'
  printf("b (main) vaut : %d\n", b)
                                 ^
2 errors generated.
$
{%endhighlight%}

Effectivement la portée de la variable `b`, déclarée dans le bloc du `if` est limitée à l'intérieur de celui-ci : on dit que c'est une *variable locale* au bloc du `if`. En commentant les lignes `12` et `13`, nous corrigeons le programme et la compilation ne renvoie plus d'erreur.

{%highlight c linenos%}
#include <stdio.h>

int main() {
  int a = 0;
  ++a;

  if (a == 1) {
    int b = 2;
    printf("a vaut : %d\n", a);
    printf("b (if) vaut : %d\n", b);
  }
  // ++b;
  // printf("b (main) vaut : %d\n", b)

  return 0;
}
{%endhighlight%}

L'execution du programme affiche le résultat suivant :

{%highlight plaintext%}
$ gcc -Wall -o run demo_portee.c
$ ./run
a vaut : 1
b (if) vaut : 2
$
{%endhighlight%}

<ul class="tips">
  <li>La variable <code>a</code>, déclarée dans le bloc de la fonction <code>main</code> est accessible partout au sein de la fonction <code>main</code>.</li>
  <li>La portée de la variable <code>b</code> est limitée dans le bloc du <code>if</code>.</li>
</ul>

Toute variable déclarée à l'intérieur d'un bloc est appelée *variable locale* au bloc. Par contre, si on veut qu'une variable soit accessible partout dans notre programme, elle doit être déclarée en dehors de tout bloc : on parle alors de *variable globale*.

Pour le moment, quand on voudra déclarer des variables globales, on le fera avant la définition de la fonction `main`.

{%highlight c linenos%}
#include <stdio.h>

int ma_var_globale = 0;

int main () {
  ++ma_var_globale;
  printf("Ma variable globale vaut : %d\n", ma_var_globale);
  return 0;
}
{%endhighlight%}

On sait qu'une variable globale est accessible partout dans notre programme. Écrivons une fonction `void incrementer()` et déplaçons la ligne `6` dans cette fonction, et finalement appelons la fonction `incrementer()` dans le main.

{%highlight c linenos%}
#include <stdio.h>

int ma_var_globale = 0;

void incrementer ();

int main () {
  incrementer();
  printf("Ma variable globale vaut : %d\n", ma_var_globale);
  return 0;
}

void incrementer () {
  ++ma_var_globale;
}
{%endhighlight%}

L'execution de notre programme affiche `Ma variable globale vaut : 1`. On a alors changé la valeur de `ma_var_globale` à l'intérieur d'une fonction. Bien qu'elle fonctionne déjà très bien, on voudrait maintenant que la fonction `incrementer()` puisse incrémenter autre chose que `ma_var_globale`. On voudrait la modifier de manière à ce qu'elle prenne en argument la variable dont on veut incrémenter la valeur. On a alors le code suivant :

{%highlight c linenos%}
#include <stdio.h>

int ma_var_globale = 0;

void incrementer ();

int main () {
  incrementer(ma_var_globale);
  printf("Ma variable globale vaut : %d\n", ma_var_globale);
  return 0;
}

void incrementer (int x) {
  ++x;
}
{%endhighlight%}

<span class="question"> Que va afficher le programme ?</span> Et bien le programme affiche `Ma variable globale vaut : 0`. En effet, en passant `ma_var_globale` en paramètre de la fonction `incrementer()`, le language `C` procède à ce que l'on appelle un *passage par valeur* ou *passage par copie*. C'est-à-dire:

<ul class="tips">
 <li>La valeur que l'on modifie dans la fonction <code>incrementer()</code> n'est pas le contenu de <code>ma_var_globale</code> mais le contenu de <code>x</code>.</li>
 <li>La variable <code>x</code> est une variable dont la valeur est une copie de la valeur de <code>ma_var_globale</code> mais à un endroit différent de la mémoire.</li>
</ul>

En mémoire cela ressemble à ça :
{%highlight plaintext%}

           x   |   0   | 102                          x |   1   | 102
               ---------                                ---------
incrementer(0) |       |                 incrementer(0) |       |
               ---------                                ---------
        main() |       |                         main() |       |
               ---------                                ---------
ma_var_globale |   0   | 80              ma_var_globale |   0   | 80   
               =========                                =========

        main() |       |
               ---------        ----> Le programme affiche : Ma variable globale vaut : 0
ma_var_globale |   0   | 80
               =========              
{%endhighlight%}

La solution pour réellement modifier la valeur passée en paramètre c'est de demander à la fonction d'aller à l'adresse mémoire où se trouve notre variable et d'y modifier sa valeur. Cela tombe bien on a vu plus haut que cela était possible avec les pointeurs. On ne va plus passer une valeur en paramètre mais plutôt une adresse. Voici donc la nouvelle version de la fonction `incrementer()`

{%highlight c%}
void incrementer (int * x) {
  ++(*x); // incrémente le contenu de la variable dont l'adresse est contenu dans x
}
{%endhighlight%}

Voici le programme entier :

{%highlight c linenos%}
#include <stdio.h>

int ma_var_globale = 0;

void incrementer (int *);

int main () {
  incrementer(&ma_var_globale); // On passe ici en paramètre l'adresse de ma_var_globale
  printf("Ma variable globale vaut : %d\n", ma_var_globale);
  return 0;
}

void incrementer (int * x) {
  ++(*x);
}
{%endhighlight%}

On appelle se que l'on vient de faire un *passage par adresse*. L'avantage c'est qu'on peut directement accéder à n'importe quelle variable, globale ou non, en passant son adresse en paramètre d'une fonction.

<br/>

À vous de jouer. Qu'affiche le programme suivant ?

{%highlight c linenos%}
#include <stdio.h>

void incrementer (int *);

int main () {
  int a = 0;
  int  *x = NULL;

  incrementer(&a);

  if (a == 1) {
    int b = 2;
    x = &b;

    printf("a : %d\n", a);
    incrementer(x);
  }

  printf("b : %d\n", *x);

  return 0;
}

void incrementer (int * x) {
  ++(*x);
}

{%endhighlight%}
