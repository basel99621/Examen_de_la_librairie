<script setup>
import { ref, defineEmits } from "vue";
// -- donnée réactive pour la saisie du titre
const titre = ref("");
const titreR = ref("");
const prix = ref(0);
const qtestock = ref(0);
const emit = defineEmits(["addC"]);
</script>

<template>
  <body>
    <div id="accueil">
      <form
        id="buttonAjouter"
        @submit.prevent="$emit('addC', titre, prix, qtestock)"
      >
        <input type="text" v-model="titre" placeholder="Nom du livre" />
        <input type="text" v-model="prix" placeholder="Prix du livre" />
        <input
          type="text"
          v-model="qtestock"
          placeholder="La quantité en stock"
        />
        <input class="buttonAjouter" type="submit" value="Ajouter" />
      </form>
      <form class="buttonRechercher" @submit.prevent="$emit('addR', titreR)">
        <input type="text" v-model="titreR" placeholder="Livre Rechercher " />
        <input class="buttoRechercher" type="submit" value="Rechercher" />
      </form>
    </div>
  </body>

  <h1 id="mesLivres">Mes livres</h1>
</template>

<style scoped>
/*Le code CSS pour l'animation du grand titre Mes livres */
#accueil {
  /* Position initiale en bas de la page */
  position: relative;
  bottom: -10px;
  /* Animation */
  animation-name: slide-up;
  animation-duration: 1.5s;
  animation-timing-function: ease-out;
  animation-fill-mode: forwards;
}
#mesLivres {
  /* Position initiale en bas de la page */
  position: relative;
  bottom: -10px;
  /* Animation */
  animation-name: slide-up;
  animation-duration: 2.5s;
  animation-timing-function: ease-out;
  animation-fill-mode: forwards;
}

/* Définition de l'animation */
@keyframes slide-up {
  /* Position initiale de l'élément */
  from {
    bottom: -100px;
  }
  /* Position finale de l'élément */
  to {
    bottom: 0;
  }
}
/* Style pour les titres h1 */
h1 {
  /* Centrer horizontalement le texte */
  display: flex;
  justify-content: center;
  /* Changer la police */
  font-family: Arial, Helvetica, sans-serif;
  /* Changer la taille de la police */
  font-size: 3em;
  /* Centrer le texte */
  text-align: center;
  /* Changer la couleur du texte */
  color: rgba(255, 64, 0, 0.826);
  /* Ajouter un effet d'ombre portée */
  text-shadow: 2px 2px 0 #fff, 4px 4px 0 #999;
  /* Ajouter un espacement entre les lettres */
  letter-spacing: 0.05em;
  /* Mettre en majuscules */
  text-transform: uppercase;
}

/* Effet hover pour les titres h1 */
h1:hover {
  /* Changer la couleur du texte */
  color: rgba(255, 217, 0, 0.751);
  /* Ajouter une transition pour l'animation */
  transition: transform 0.5s ease-out;
  /* Ajouter un déplacement du titre au survol */
  transform: translate(10px, -10px);
}

/* Style pour le corps de la page */
body {
  /* Centrer horizontalement et verticalement */
  display: flex;
  align-items: center;
  justify-content: center;
  /* Définir la hauteur minimale de la page */
  min-height: 10vh;
  /* Définir la couleur de fond */
  background-color: rgba(255, 255, 255, 0.847);
}

/* Style pour le formulaire */
form {
  /* Centrer horizontalement */
  display: flex;
  justify-content: center;
  align-items: center;
  /* Définir la largeur du formulaire */
  width: 80%;
  max-width: 800px;
  /* Définir la marge */
  margin: 1em 0;
}

/* Style pour les champs de saisie */
input {
  /* Définir la marge et le rembourrage */
  margin: 0.5em;
  padding: 0.5em;
  /* Changer la taille de la police */
  font-size: 1em;
  /* Supprimer les bordures */
  border: none;
  /* Arrondir les bords */
  border-radius: 0.25em;
  /* Ajouter une ombre portée */
  box-shadow: 0 0 0.5em rgba(0, 0, 0, 0.1);
}

/* Style pour les boutons "Ajouter" et "Rechercher" */
.buttonAjouter,
.buttoRechercher {
  /* Changer la couleur du texte */
  color: rgba(255, 255, 255, 0.607);
  /* Ajouter une bordure */
  border: 1px solid #ccc;
  /* Définir la taille du rembourrage */
  padding: 3px 5px;
  /* Arrondir les bords */
  border-radius: 5px;
  /* Supprimer le soulignement du texte */
  text-decoration: none;
  /* Changer la taille de la police */
  font-size: 16px;
  /* Mettre en majuscules */
  text-transform: uppercase;
  /* Ajouter une ombre portée */
  box-shadow: 0px 0px 5px;
  background: linear-gradient(to bottom right, #4f3c03, #ff545475);
  text-transform: uppercase;
}

.buttoRechercher:hover {
  transform: scale(1.2);
}
.buttonAjouter:hover {
  transform: scale(1.2);
}
div {
  display: flex;
}
</style>
