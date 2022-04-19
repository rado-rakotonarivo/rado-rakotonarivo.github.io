---
layout: post
title:  "Centrer des éléménts [Prog HTML]"
# published: false
categories: teaching html
---

<style>
.box-1 {
  background: #ffeaa7;
  margin-top: 2em;
  margin-bottom: 2em;
  padding-top: 1em;
  padding-bottom: 1em;
}

.box-2 {
  background: #e17055;
  width: 70%;
  padding: .75em;
}

.box-2:nth-child(2) {
  background: #55efc4;
}

.margin-centered .box-2 {
  margin-left: auto;
  margin-right: auto;
}

.flex-centered {
  display: flex;
  flex-direction: column;
  align-items: center; /*centre selon les lignes*/
}

.box-2 p {
  background: #dfe6e9;
  opacity: .75;
  text-align: justify;
}

.box-sizing-content-box {
  box-sizing: content-box;
}

.box-sizing-border-box {
  padding: .75em;
}

</style>

<h2 class="listing">Centrer des éléments html</h2>

Considérons le code html suivant :

{% highlight html linenos%}
<div class="box-1">
  <div class="box-2">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
      incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
      exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
      dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
  <div class="box-2">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
      incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
      exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
      dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
</div>

{% endhighlight %}

Notre objectif sera de centrer les deux <code>div</code> de classe <code>.box-2</code> dans leur conteneur <code>.box-1</code>. Puis, de centrer les paragraphes à l'intérieur des <code>.box-2</code>. Pour finalement obtenir le résultat d'affichage suivant:

<div class="box-1 margin-centered">
  <div class="box-2">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
  <div class="box-2">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
</div>

Les règles <code>css</code> suivantes permettent d'appliquer des couleurs de fond à nos <code>div</code> ainsi qu'aux paragraphes. Et en même temps de centrer les paragraphes dans les <code>.box-2</code>.

{% highlight css %}
.box-1 {
  background: #ffeaa7;
  padding-top: 1em;
  padding-bottom: 1em;
}

.box-2 {
  background: #e17055;
  width: 70%;
  padding: .75em; /* Mettre une seule valeur pour toutes les marges intérieurs permet de centrer le contenu*/
}

.box-2 p {
  background: #dfe6e9;
  opacity: .75;
  text-align: justify;
}

{% endhighlight %}

<div class="box-container">
  <h3>Non centré</h3>
  <div class="box-1 non-centered">
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
  </div>
  <h3>Centrer avec <code>margin: auto;</code></h3>
  <ul>
      <li>Spécifier une <code>width</code> pour l'élément</li>
      <li>Définir <code>margin: auto;</code> pour l'élément</li>
  </ul>
  <div class="box-1 margin-centered">
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
  </div>
  <h3>Centrer avec <code>display: flex;</code></h3>
  <ul>
    <li>Mettre le conteneur en <code>display: flex;</code></li>
    <li>Disposer les éléménts en colonnes</li>
    <li>Centrer par rapport à l'axe des lignes <code>align-items: center;</code></li>
  </ul>
  <div class="box-1 flex-centered">
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
    <div class="box-2">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      </p>
    </div>
  </div>
</div>

<h2 class="listing" >Le box-sizing</h2>
<p>Cette propriété ayant pour valeur par défaut <code>content-box</code> permet de spécifier si la taille donnée à l'élément s'applique uniquement sur son contenu ou doit prendre en compte les marges intérieures et les bordures.</p>

<p>Par exemple les deux <code>div</code> suivantes sont de même largeur et même hauteur: (imaginons 500px x 150px)</p>

<ul>
  <li>La première est en <code>box-sizing: border-box;</code>, la largeur 500px comprend à la fois le contenu, le padding et la taille des bordures</li>
  <li>La deuxième est en <code>box-sizing: content-box;</code> : 500px est la largeur disponible pour le contenu.</li>
</ul>
<div class="box-1 margin-centered">
  <div class="box-2 box-sizing-border-box">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
  <div class="box-2 box-sizing-content-box">
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
</div>
