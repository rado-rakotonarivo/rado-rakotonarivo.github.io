---
layout: post
title:  "Correction TD2 L1Info Prog 1"
categories: teaching pro-1
---

[<< Retour](/teaching)

Vous trouverez les énoncés sur le moodle du cours [ici](https://moodlelms.univ-paris13.fr/course/view.php?id=1394).

### TD 2 : premiers pas en C

---

#### Identificateurs

---

- Un `identificateur` en C sert à identifier une variable (mais pas que ... on verra plus tard qu'il peut aussi à identifier autre chose qu'une variable), ou plus simplement la nommer. Il renseigne au programme à quel endroit de la mémoire récupérer la valeur de la variable qu'il identifie

- Il est donc important de bien nommer nos variables. Pour cela il existe quelques règles à respecter :

  -- Un identificateur doit être une suite de lettres (sans caractère accentué) et/ou de chiffres, l'unique autre caractère autorisé est l'underscore : `'_'`.

  -- Un identificateur doit obligatoirement commencer par une lettre, mais peut également commencer par un underscore.

  -- Un identificateur ne peut être un mot-clé du langage (par exemple: int ou main ne sont pas valides)

 Donc ici `rendez_vous` est valide tandis que `1par1` ne l'est pas car commence par un chiffre et `else` non plus puisque c'est un mot-clé du langage.

---
#### Déclaration et affectation de variables impératives
---

- Une `affectation` de variable signifie _donner/assigner_ une valeur à une variable.
- Le signe de l'affectation en C est le signe `'='`. La partie à gauche du signe d'affectation doit désigner une variable tandis que celle à droite est une expression dont la valeur sera évaluée et affectée dans la variable de gauche.

Du coup pour la question 1, j'ai mis en commentaire ce que fait le programme.

{% highlight javascript %}
document.write("JavaScript is a simple language for javatpoint learners");
{% endhighlight %}
