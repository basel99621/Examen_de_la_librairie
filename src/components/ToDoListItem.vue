<script setup>
import { defineEmits, defineProps } from "vue";
const props = defineProps(["livre"]);
const emit = defineEmits(["deleteC", "augmenter", "diminuer"]);

const diminuer = () => {
  emit("diminuer", props.livre);
};
const augmenter = () => {
  emit("augmenter", props.livre);
};
</script>

<template>
  <ul>
    <li>
      <div class="book">
        <h2>Titre : {{ livre._titre }}</h2>
        <h2>La quantité : {{ livre._qtestock }}</h2>
        <h2>Le prix : {{ livre._prix }} €</h2>
      </div>

      <div class="buttonBas">
        <!-- cette fois sen param du handler 
          on n'utilise pas l'index dans la tableau 
          mais directement l'id du livre à supprimer
    -->
        <button class="buttonSup" @click="$emit('deleteC', livre.id)">
          Supprimer
        </button>

        <button class="buttonDim" type="button" @click="diminuer">-</button>
        <span class="qt">{{ livre._qtestock }}</span>
        <button class="buttonAug" type="button" @click="augmenter">+</button>
      </div>
    </li>
  </ul>
</template>

<style>
/* Je n'ai pas utilisé scoped pour ne pas que le code CSS soit limité aux éléments de ce composannt et pour une meilleure mise en page*/

/*code pour l'animation de l'affichage du div book*/
.book {
  /* Position initiale en bas de la page */
  position: relative;
  bottom: -100px;
  /* Animation */
  animation-name: slide-up;
  animation-duration: 3.5s;
  animation-timing-function: ease-out;
  animation-fill-mode: forwards;
}
.buttonBas {
  /* Position initiale en bas de la page */
  position: relative;
  bottom: -100px;
  /* Animation */
  animation-name: slide-up;
  animation-duration: 2s;
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

/* Styles pour la classe .book qui représente chaque livre */
.book {
  /* Dimensions et marges du livre */
  width: 210px;
  height: 270px;
  padding-left: 10px;
  margin: 20px;
  /* Ombre et arrondi des coins */
  box-shadow: 10px 10px 10px rgba(227, 227, 227, 0.724);
  border-radius: 10px;
  /* Positionnement relatif pour contenir les éléments enfants */
  position: relative;
  /* Masquage des éléments qui débordent */
  overflow: hidden;
  /* Affichage en tant que conteneur de type flex */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* Dégradé de couleurs de fond */
  background: linear-gradient(to bottom right, #d6a504, #030202);
  /* Police et couleur de texte */
  font-family: Arial, Helvetica, sans-serif;
  color: rgba(255, 251, 19, 0.553);
  /* Ombre de texte et contour */
  text-shadow: 0px 0px 2px whitesmoke;
  -webkit-text-stroke: 1px black;
  /* Bordures gauche et bas */
  border-left: 10px solid rgba(8, 8, 8, 0.237);
  border-bottom: 5px solid rgba(0, 0, 0, 0.662);
}
/* Styles au survol du livre */
.book:hover {
  /* Agrandissement du livre */
  transform: scale(1.1);
}

/* Styles pour les citations représentées par la classe .qt qui représente l'espace où on a le nombre des livres */
.qt {
  /* Bordure, couleur de texte, et espacement intérieur */
  border: solid;
  color: rgba(255, 255, 255, 0.607);
  padding: 5px;
  /* Dégradé de couleurs de fond */
  background: linear-gradient(to bottom right, #4f3c03, #ff545475);
}
/* Styles au survol de la citation */
.qt:hover {
  /* Agrandissement de la citation */
  transform: scale(1.1);
}

/* Styles pour la liste représentée par la balise ul */
ul {
  /* Suppression des puces et des marges par défaut */
  list-style: none;
  margin: 0;
  padding: 0;
  /* Affichage en tant que conteneur de type flex */
  display: flex;
  /* Permettre à la ligne de se casser pour les écrans plus petits */
  flex-wrap: wrap;
  /* Centrer les livres horizontalement sur la page */
  justify-content: center;
}
li {
  margin: 10px; /* ajouter un peu d'espace entre les livres */
}
.buttonBas {
  list-style: none;
  display: flex; /* afficher les livres en tant que flex container */
  flex-wrap: wrap; /* permettre à la ligne de se casser pour les écrans plus petits */
  justify-content: center; /* centrer les livres horizontalement sur la page */
  display: flex;
  gap: 10px; /* Espacement entre les boutons */
}
/* Définir le style des boutons */
.buttonAug,
.buttonSup,
.buttonDim {
  /* Couleur de texte et bordure des boutons */
  color: rgba(255, 255, 255, 0.607);
  border: 1px solid #ccc;
  /* Rembourrage et rayon de bordure des boutons */
  padding: 3px 5px;
  border-radius: 5px;
  /* Style de texte des boutons */
  text-decoration: none;
  font-size: 16px;
  text-transform: uppercase;
  /* Ombre portée autour des boutons */
  box-shadow: 0px 0px 5px;
  /* Dégradé de couleur de fond des boutons */
  background: linear-gradient(to bottom right, #4f3c03, #ff545475);
}

/* Effet de survol pour les boutons de suppression, augmentation et diminution */
.buttonSup:hover,
.buttonAug:hover,
.buttonDim:hover {
  /* Agrandir légèrement le bouton au survol */
  transform: scale(1.1);
}

/* Style de la liste des boutons */
.buttonBas {
  /* Ne pas afficher les puces de la liste */
  list-style: none;
  /* Afficher les boutons en tant que conteneur flexible */
  display: flex;
  /* Permettre à la ligne de se casser pour les écrans plus petits */
  flex-wrap: wrap;
  /* Centrer horizontalement les boutons sur la page */
  justify-content: center;
  /* Espacement entre les boutons */
  gap: 10px;
}
</style>
