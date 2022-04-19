---
layout: post
title:  "Correction TP3 [Prog 1]"
categories: teaching prog-1
---

<p>Vous trouverez les énoncés des TD sur le moodle du cours <a href="https://moodlelms.univ-paris13.fr/course/view.php?id=1394">ici</a>.</p>

<h2 class="listing">TP 3 : boucle <i>while</i>; expressions booléennes; type de données </h2>

<h3>Évaluation d'expressions booléennes</h3>

<ul class="tips">
  <li>
    Une variable de type <code>booléenne</code> est une variable qui ne peut admettre que deux valeurs : soit <code>VRAI</code>, soit <code>FAUX</code>.
  </li>
  <li>
    Très souvent, on codera une variable booléenne comme étant un entier dont la valeur est soit <code>1</code> pour <code>VRAI</code>, soit <code>0</code> pour <code>FAUX</code>.
  </li>
  <li>
    De manière simple, une <code>expression booléenne</code> est une expression qui donne une valeur booléenne.
  </li>
</ul>

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

int main () {
  /* EXERCICE 3 : Evaluation d'expression booleene */

  printf("EXERCICE 3 : Evaluation d'expression booleene\n");

  int a, b; // nos variables booleenes

  printf("Entrez deux variables booleenes : ");
  scanf("%d %d", &a, &b);

  // affichage: on utilise \t pour afficher une tabulation
  printf("a\tb\ta et b\ta ou b\tNON a\tNON b\tNON a ET b\n");
  printf("%d\t%d\t%d\t%d\t%d\t%d\t%d\n", a, b, a && b, a || b, !a, !b, !a && b);

  return EXIT_SUCCESS;
}

{% endhighlight %}

<h3>Type de données</h3>

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int main () {

  /* EXERCICE 5 : Polynome */

  printf("EXERCICE 5 : Polynome\n");

  double x = 0.707107;
  double poly = 8118 * pow(x,4) - 11482 * pow(x,3) + pow(x,2) + 5741 * x - 2030;
  printf("poly vaut : %f\n", poly);

  // On obtient toujours 0 à cause des arrondis et du manque de précision
  // Ne pas oublier l'option -lm à la compilation pour utiliser la bibliothèque <math.h>

  return EXIT_SUCCESS;
}

{% endhighlight %}

<h3>Fibonacci</h3>

Pour une petite documentation et retrouver les valeur de la suite, allez [ici]("https://fr.wikipedia.org/wiki/Suite_de_Fibonacci").

{% highlight c linenos %}

#include <stdio.h>
#include <stdlib.h>

int main () {

  /* EXERCICE 6 : Suite de Fibonacci */

  printf("EXERCICE 6 : Suite de Fibonacci\n");

  // fibo (n) =   | 1 si n == 1 ou n == 2
  //              | fibo (n-1) + fibo (n-2) sinon

  // Pour l'instant nous n'allons pas écrire de fonction (on va faire une boucle)

  // question 1 : boucle for

  int u1 = 1, u2 = 1, u3 = 0;
  int n = 0;

  printf("Entrez la valeur de n (>= 3): ");
  scanf("%d", &n);


  for (int i = 2; i < n; ++i) {
    u3 = u1 + u2; // c'est comme si on disait u_i = u_{i-1} + u_{i-2}
    printf("f(%d) = %d\n", i + 1, u3);
    u1 = u2;  // puis pour la prochaine itération on décale les termes de 1
    u2 = u3;
  }
  printf("Fibo(%d) vaut : %d\n", n, u3);

  // question 2 : boucle while
  // L'utilisateur entre un entier m, on veut afficher fibo(n) et n tel que fibo(n) <= m

  int m = 0;
  u1 = 1, u2 = 1, u3 = 0;

  printf("\nEntrez la valeur de m (>=2): ");
  scanf("%d", &m);

  int rang = 2;

  while (u3 <= m) {
    u3 = u1 + u2;
    u1 = u2;
    u2 = u3;
    ++rang;
  }
  // quand on sortira de la boucle cela veut dire que nous avons fibo(n) > m,
  // il nous faut donc afficher n-1 et fibo(n-1)
  // n-1 vaut rang-1 et fibo(n-1) vaut u1
  printf("Valeur du terme inferieur a %d : %d de rang %d\n", m, u1, rang-1);

  return EXIT_SUCCESS;
}

{% endhighlight %}
