# OFFCANVAS COMPONENT CSS ONLY DEMO PAGE

Popularisé par les applications smartphone.
Nous allons découvrir comment le réaliser sans JS!.
Less is more, cela permet de décharger le navigateur des taches JS en utilisant seulement le CSS.

## Objectifs et défis

- Créez un espace d'écran supplémentaire en masquant la navigation.
- Accédez facilement au menu en cliquant sur l'icône hors toile et en la faisant glisser en place.
- Seul le CSS sera utilisé pour l'effet
- Prend en charge autant de navigateurs que possible

### Le balisage

En commençant par un wrapper div

```
<div class="wrapper"> 
 <aside>
  <nav> 
   <ul> 
    <li>nav_1</li>
    <li>nav_2</li>
    <li>nav_3</li>
    <li>nav_4</li>
    <li>nav_5</li>
   </ul> 
  </nav> 
 </aside> 
</div>
```

### le contenu du site

Le contenu du site est contenu dans une section

```
<section>
  <div class="container">
    <div class="row">
      <h2>Lorem ipsum dolor sit amet.</h2>
      <p>Lorem ipsum......</p>
    </div>
    <!--- add content --->
  </div>
</section>
```

### Le CSS

J'ai conservé le CSS en ligne pour le garder concis, mais il peut facilement faire partie d'un script externe.

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  font-size: 63.5%;
  font-family: "Roboto Slab", serif;
  height: 100%;
}
body {
  font-size: 1.6rem;
  line-height: 2.8rem;
  height: 100%;
}
.wrapper {
  height: 100%;
}
.container {
  margin: 0 15px;
}
.row {
  padding: -15px;
  margin: 15px 0;
}
.row:before,
.row:after {
  content: "";
  display: table;
}
nav li {
  padding: 8px;
}

```

Maintenant que les styles initiaux sont en place, nous allons nous occuper des deux éléments principaux. 
Pour la barre latérale (OFFCANVAS) , nous allons définir une largeur initiale de 40 %, la faire flotter à gauche et la positionner hors de l'écran avec une marge gauche de -40 %, et nous allons également ajouter une position absolue pour éviter qu'elle ne s'empile sur le contenu principal.

```

aside {
  position: absolute;
  top: 0;
  left: -40%;
  width: 40%;
  height: 100%;
  background: #333;
  transition: all 0.3s ease-in-out;
  }
```

Pour l'élément de section qui contient le contenu principal, nous allons le faire floater à droite avec une largeur et une hauteur de 100 % et une marge droite de 0.

```
 section{
  width: 100%;
  height: 100%;
  float: right;
  margin-right: 0;
}
```

Ajoutons maintenant une case à cocher en haut de notre balisage, juste avant la div wrapper.
```
<input type="checkbox" id="offcanvas" class="toggle" />
<div class="wrapper"><!--- wrapper content here ---></div>
```

Nous lui avons donné un id #offcanvas qui sera utilisé plus tard par les tag pour déclencher le basculement.
Maintenant, nous voulons réagir à l'état coché de l'entrée et afficher la navigation lorsqu'elle est cochée et la cacher à nouveau lorsqu'elle est décochée.

Nous utiliserons le sélecteur adjacent ( + ) dans notre CSS et ciblerons d'abord l'élément de côté.

```
.toggle:checked + .wrapper > aside {
  margin-left: 0;
}
```

et de même pour l'élément de section

```
.toggle:checked + .wrapper > section {
  margin-right: -40%;
}
```

### Make It Pretty

L'objectif principal est de masquer et d'afficher la navigation. Nous allons simplement rendre les choses un peu plus agréables en ajoutant le fameux bouton "hamburger" et en faisant en sorte que la transition se fasse en douceur.

Ajoutons un `label` qui contiendra le bouton et qui déclenchera le basculement. 
En haut de l'élément section, ajoutons ce code :

```
<div class="container">
  <div class="row">
    <label for="offcanvas" class="toggler">
      <span class="navicon"></span>
    </label>
  </div>
</div>
```

Le `label` et son l'attribut `for` a une valeur "offcanvas" qui est la même que l'identifiant de notre bouton de saisie, ce qui nous permet de déclencher le basculement à partir de n'importe quel endroit de la page où le code de l'étiquette existe. 

Ajoutons maintenant quelques styles.

```
.toggler {
  display: inline-block;
  cursor: pointer;
}
.navicon {
  width: 28px;
  height: 28px;
  background: url("navicon.png") no-repeat;
  background-size: cover;
  display: block;
}
```

Nous pouvons cacher le input

```
.toggle {
  display: none;
}
```

### Un grand succès 

Lorsque la navigation est affichée, la seule façon de la cacher à nouveau est d'appuyer précisément sur le bouton du menu. Cela peut convenir sur un écran d'ordinateur de bureau, mais peut être difficile sur des résolutions plus petites. Nous allons rendre l'ensemble du contenu cliquable pendant cet état pour atténuer ce problème. Donc, revenons au code html avant la première étiquette, nous allons en ajouter une autre.

```
<section>
  <label for="offcanvas" class="biglabel"></label>
  <!--- section content --->
</section>
```

Nous lui avons donné la classe ".biglabel". 
Dans notre CSS, nous allons le cacher lorsque la navigation est masquée et de faire couvrir l'ensemble du contenu comme un gros bouton.

```
.toggle,
.biglabel {
  display: none;
}
.biglabel {
  width: 100%;
  height: 100%;
  position: absolute;
  cursor: pointer;
}
.toggle:checked + .wrapper > section .biglabel {
  display: block;
}
```
Lorsque nous actualisons le navigateur, nous constatons que l'ensemble du contenu devient cliquable lorsque la navigation est affichée. 

Parfait !
La dernière étape consiste à gérer la transition et à faire glisser joliment la navigation. 

L'utilisation de la transition CSS3 rend les choses très faciles. Nous allons cibler à la fois la barre latérale et le contenu principal.
```
aside,
section {
  -webkit-transition: margin 0.5s ease-in-out;
  -moz-transition: margin 0.5s ease-in-out;
  -ms-transition: margin 0.5s ease-in-out;
  -o-transition: margin 0.5s ease-in-out;
  transition: margin 0.5s ease-in-out;
}
```

👩🏻‍💻 Happy Coding !
