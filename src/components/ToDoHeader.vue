
<template>
  <header>
    <div class="Bienvenue">
      <img
        id="logo"
        src="https://th.bing.com/th/id/R.777a724279a813f1a14ebb55c79a21c7?rik=FxILDSXK6whCpQ&riu=http%3a%2f%2fwww.clipartbest.com%2fcliparts%2fncB%2f6Lq%2fncB6LqRcA.jpeg&ehk=58qsQ%2bjL5UrV7094bQo1%2f4FPqS4lCu8ea5jg4fW%2bYRo%3d&risl=&pid=ImgRaw&r=0"
        alt="logo"
        height="90px"
        width="90px"
      />
      <h3>Bienvenue dans la librairie de BASEL AL KHATIB</h3>
    </div>
    <nav>
      <ul>
        <li><a href="#accueil">Accueil</a></li>
        <li><a href="#mesLivres">Mes livres</a></li>
        <li><a href="#propos">A propos</a></li>
        <li><a href="#contact">connexion</a></li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
/* Les animations*/
h3 {
  animation: typing 3s steps(20) forwards;
  white-space: nowrap;
  overflow: hidden;
}

@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}
ul li {
  opacity: 0;
  transform: translateY(20px);
  animation-name: fadeInUp;
  animation-duration: 0.6s;
  animation-fill-mode: forwards;
}

ul li:nth-child(1) {
  animation-delay: 1s;
}

ul li:nth-child(2) {
  animation-delay: 2s;
}

ul li:nth-child(3) {
  animation-delay: 3s;
}

ul li:nth-child(4) {
  animation-delay: 4s;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
/*Pour éviter d'abîmer la mise en page lorsqu'on réduit la fenêtre*/
/* Appliquer des styles différents lorsque la largeur de l'écran est inférieure ou égale à 600px */
@media only screen and (max-width: 600px) {
  /* Changer la direction de l'agencement en colonne pour le header */
  header {
    flex-direction: column;
    height: auto;
  }

  /* Masquer la navigation */
  nav {
    display: none;
  }

  /* Afficher la navigation lorsqu'elle est active */
  nav.show {
    display: flex;
    flex-direction: column;
    text-align: center;
  }

  /* Ajouter une marge aux éléments de la navigation */
  nav.show li {
    margin: 10px 0;
  }

  /* Ajouter des styles pour l'icône de menu */
  .menu-icon {
    cursor: pointer;
    display: block;
    padding: 28px 20px;
    position: relative;
    user-select: none;
  }

  /* Ajouter des styles pour les éléments de l'icône de menu */
  .menu-icon .navicon {
    background: #fff;
    display: block;
    height: 2px;
    position: relative;
    transition: background 0.2s ease-out;
    width: 18px;
  }

  /* Ajouter des styles pour les éléments de l'icône de menu avant et après */
  .menu-icon .navicon:before,
  .menu-icon .navicon:after {
    background: #fff;
    content: "";
    display: block;
    height: 100%;
    position: absolute;
    transition: all 0.2s ease-out;
    width: 100%;
  }

  /* Ajouter des styles pour l'élément de menu avant */
  .menu-icon .navicon:before {
    top: 5px;
  }

  /* Ajouter des styles pour l'élément de menu après */
  .menu-icon .navicon:after {
    top: -5px;
  }

  /* Masquer le bouton de menu */
  .menu-btn {
    display: none;
  }

  /* Masquer le menu lorsqu'il n'est pas activé */
  .menu-btn:checked + .menu {
    display: none;
  }

  /* Ajouter des styles pour l'icône de menu lorsqu'elle est active */
  .menu-btn:checked + .menu-icon .navicon {
    background: transparent;
  }

  /* Ajouter des styles pour l'élément de menu avant lorsqu'il est activé */
  .menu-btn:checked + .menu-icon .navicon:before {
    transform: rotate(-45deg);
  }

  /* Ajouter des styles pour l'élément de menu après lorsqu'il est activé */
  .menu-btn:checked + .menu-icon .navicon:after {
    transform: rotate(45deg);
  }

  /* Ajouter des styles pour les éléments de l'icône de menu avant et après lorsqu'ils sont activés */
  .menu-btn:checked + .menu-icon:not(.steps) .navicon:before,
  .menu-btn:checked + .menu-icon:not(.steps) .navicon:after {
    top: 0;
  }
}

/*le reste du code CSS pour le design et la decoration et que j'ai délà commenté dans les autres composants*/
.Bienvenue {
  color: wheat;
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
  font-size: 18px;
  display: flex;
  align-items: center; /* Pour centrer horizontalement */
  justify-content: center; /* Pour centrer verticalement */
  height: 50%; /* Hauteur de l'élément parent */
  text-transform: uppercase;
}
.Bienvenue h3:hover {
  color: gold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5), 0 0 20px gold;
}

#logo {
  margin-right: 10px;
}

body {
  font-family: "Arial";
  font-size: 0.8em;
  padding: 0;
  margin: 0;
  color: #ffffff;
  background-color: rgb(228, 250, 255);
}

ul {
  margin-left: 0px;
  display: flex;
  text-align: right;
  margin: 0px;
  padding: 0px;
}

header {
  background-color: #fbb9367f;
  display: flex; /* permet d'utiliser les propriétés align-items et justify-content */
  align-items: center; /* aligne verticalement les éléments */
  justify-content: space-between; /* aligne horizontalement les éléments */
  background: linear-gradient(to bottom right, #4f3c03, #ff545475);
}
nav {
  display: flex;
  justify-content: flex-end;
}

li {
  display: inline-block;
  list-style-type: none;
}
a {
  text-decoration: none;
  font-family: "Arial";
  color: wheat;
  text-transform: uppercase;
  font-size: 1.2em;
  padding: 0px 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-shadow: 0px 0px 10px rgb(0, 0, 0);
}
ul li a:hover {
  color: gold;
}
ul li a:hover {
  transform: scale(1.3);
}

#monImage {
  display: flex;
  text-align: left;
}
</style>

