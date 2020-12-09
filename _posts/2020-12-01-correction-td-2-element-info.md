---
layout: post
title:  "Correction TD2 [Prog 1]"
categories: teaching prog-1
---

[<< Retour](/blog)

<p>Vous trouverez les énoncés des TD sur le moodle du cours <a href="https://moodlelms.univ-paris13.fr/course/view.php?id=1394">ici</a>.</p>


<h2 class="listing"> TD 2 : premiers pas en C </h2>

<h3> Identificateurs </h3>

<p>Un <code>identificateur</code> en C sert à identifier une variable (mais pas que ... on verra plus tard qu'il peut aussi à identifier autre chose qu'une variable), ou plus simplement la nommer. Il renseigne au programme à quel endroit de la mémoire récupérer la valeur de la variable qu'il identifie. Il est donc important de bien nommer nos variables. Pour cela il existe quelques règles à respecter :
</p>

<ul class="tips">
  <li>
    Un identificateur doit être une suite de lettres (sans caractère accentué) et/ou de chiffres, l'unique autre caractère autorisé est l'underscore : <code>_</code>.
  </li>  
  <li>
    Un identificateur doit obligatoirement commencer par une lettre, mais peut également commencer par un underscore.
  </li>
  <li>
    Un identificateur ne peut être un mot-clé du langage (par exemple: int ou main ne sont pas valides)
  </li>
</ul>  

 Donc ici <code>rendez_vous</code> est valide tandis que <code>1par1</code> ne l'est pas car commence par un chiffre et <code>else</code> non plus puisque c'est un mot-clé du langage.

<h3>Déclaration et affectation de variables impératives</h3>

<ul class="tips">
  <li>
    Une <code>affectation</code> de variable signifie <em>donner/assigner</em> une valeur à une variable.
  </li>
  <li>
    Le signe de l'affectation en C est le signe <code>=</code>. La partie à gauche du signe d'affectation doit désigner une variable tandis que celle à droite est une expression dont la valeur sera évaluée et affectée dans la variable de gauche.
  </li>
</ul>  
Du coup pour la question 1, j'ai mis en commentaire ce que fait le programme.


{% highlight c linenos %}

#include <stdlib.h>
#include <stdio.h>

int main() {

int x; // déclaration d'un variable de type entière x
x = 3; // affectation de la valeur 3 dans x
x = x + 1; // affectation de la dernière valeur de x plus 1 dans x
printf("x = %d\n", x); // affiche à l'écran x = 4

return EXIT_SUCCESS;
}

{% endhighlight %}

<h3>Trace d'un programme</h3>

<p>Il s'agit de faire une simulation d'execution du programme dans un tableau : c'est-à-dire regarder ligne par ligne quels sont les valeurs successives que prennent nos variables. On peut également afficher ce qui sort à l'écran.</p>

{% highlight plaintext %}
  lignes | x | Sortie écran
  -----------------------------
     6   | ? |
     7   | 3 |
     8   | 4 |
     9   |   | x = 4
  -----------------------------
    11   | Renvoie EXIT_SUCCESS
{% endhighlight %}

<h3>Ecriture d'un programme</h3>
<ul class="tips">
  <li>On va procéder à peu près de cette manière pour tout le cours. Pour chaque problème donné en TD: proposer un algorithme, écrire en C le programme correspondant, puis en faire la trace.</li>
  <li>Écrire un algorithme revient à écrire des phrases en français qui décrit les étapes à suivre pour résoudre le problème.</li>
  <li>Un algorithme peut prendre quelque chose en entrée et renvoyer quelque chose en sortie. Par exemple un algorithme de tri peut prendre un tableau en entrée et renvoyer un tableau trié. Mais il peut également ne rien prendre en entrée ni rien renvoyer en sortie. Par exemple un algorithme qui permet d'afficher 100 fois le mot "bonjour". Il faut faire la différence entre <em>Renvoyer</em> et <em>Afficher</em>.</li>
</ul>
<p>Dans notre exercice, l'algorithme ne prend rien en entrée car la valeur dont on va calculer le carré et le cube sera directement initialisée dans notre algo. Il ne renvoie rien en sortie, on affichera juste un résultat.</p>

{% highlight plaintext %}
Algorithme : Calcule le carré et le cube d'une valeur contenue dans une variable
Entrées : Rien
Sorties : Rien
début:
  soit x un entier, carre un entier, cube un entier
  x <- 2
  carre <- x * x
  cube <- carre * x
  afficher ("x^2 = carre et x^3 = cube")
:fin
{% endhighlight %}

<p>Ensuite, pour écrire le code correspondant, il faudra transcrire ligne par ligne notre algorithme en langage C.</p>

{% highlight c linenos %}
#include<stdio.h>
#include<stdlib.h>

int main() {
  int x, carre, cube;
  x = 2;
  carre = x * x;
  cube = carre * x;
  printf("x^2 = %d et x^3 = %d\n", carre, cube)
  return EXIT_SUCCESS;
}
{% endhighlight %}


<h5>Trace du programme</h5>
<p>Je vous laisse le soin de faire la trace du programme :).</p>
