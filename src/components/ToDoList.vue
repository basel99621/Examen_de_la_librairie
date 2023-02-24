<template>
  <ToDoForm @addC="handlerAdd" @addR="rechercheLivres"></ToDoForm>
  <ul>
    <ToDoListItem
      v-for="livre of listeL"
      :key="livre.id"
      :livre="livre"
      @deleteC="handlerDelete"
      @augmenter="handlerAugmenter"
      @diminuer="handlerDiminuer"
    />
  </ul>
</template>

<script setup>
import { reactive, onMounted, defineExpose } from "vue";
import ToDoListItem from "./ToDoListItem.vue";
import ToDoForm from "./ToDoForm.vue";
import Livre from "../Livre";

// Création d'un objet réactif vide pour stocker la liste de livres
const listeL = reactive([]);

// -- l'url de l'API
const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/3/livres";

// -- handler pour supprimer un livre à partir de son id
function handlerDelete(id) {
  console.log(id);
  const fetchOptions = {
    method: "DELETE",
  };
  // -- l'id du livre à supprimer doit être
  //  ajouté à la fin de l'url
  fetch(url + "/" + id, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getLivres();
    })
    .catch((error) => console.log(error));
}
// -- handler pour ajouter un nouveau livre à partir de son titre
function handlerAdd(titre, prix, qtestock) {
  console.log(titre, prix, qtestock);
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // --  le titre du noiuveau livre est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({ titre: titre, qtestock: qtestock, prix: prix }),
  };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getLivres();
    })
    .catch((error) => console.log(error));
}

// -- req AJAX pour récupérer les livres
//    et les stocker dans le state listeL
function getLivres() {
  const fetchOptions = { method: "GET" };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      // -- vider la liste des livres
      listeL.splice(0, listeL.length);
      // pour chaque donnée renvoyée par l'API
      //  créer un objet instance de la classe Livre
      //  et l'ajouter dans la liste listeL
      dataJSON.forEach((v) =>
        listeL.push(new Livre(v.id, v.titre, v.qtestock, v.prix))
      );
    })
    .catch((error) => console.log(error));
}

// -- appel de la req AJAX une fois après la création de l'instance
onMounted(() => {
  getLivres();
});

function rechercheLivres(titre) {
  console.log("Je recherche !!!!!!", titre);
  // - l'url (la route) pour la recherche de livres n'est pas la même
  const urlLivres =
    "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/3/livres?search=";
  const fetchOptions = { method: "GET" };
  // récupérer la valeur saisie dans la zone de texte

  // --- la valeur saisie doit être ajoutée à la fin de l'URL
  fetch(urlLivres + titre, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      // -- vider la liste des livres
      listeL.splice(0, listeL.length);
      // pour chaque donnée renvoyée par l'API
      //  créer un objet instance de la classe Livre
      //  et l'ajouter dans la liste listeL
      dataJSON.forEach((v) =>
        listeL.push(new Livre(v.id, v.titre, v.qtestock, v.prix))
      );
    })
    .catch((error) => console.log(error));
}

//pour auhgmenter la quantité des livres
function handlerAugmenter(livre) {
  // affiche une copie de l'objet livre dans la console
  console.log({ ...livre });

  // appelle la méthode "augmenter" de l'objet livre
  livre.augmenter();

  // affiche une nouvelle copie de l'objet livre dans la console
  console.log({ ...livre });

  // crée un nouvel objet "Headers"
  let myHeaders = new Headers();

  // ajoute un en-tête "Content-Type" à l'objet Headers
  myHeaders.append("Content-Type", "application/json");

  // définit l'URL de l'API à appeler
  const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/3/livres";

  // crée un objet "fetchOptions" contenant les options pour la requête HTTP
  const fetchOptions = {
    method: "PUT", // méthode HTTP pour mettre à jour une ressource
    headers: myHeaders, // en-têtes de la requête
    body: JSON.stringify({
      // corps de la requête sous forme de chaîne JSON
      id: livre.id, // id du livre à mettre à jour
      titre: livre.titre, // nouveau titre du livre
      prix: livre.prix, // nouveau prix du livre
      qtestock: livre.qtestock, // nouvelle quantité en stock du livre
    }),
  };

  // envoie la requête HTTP à l'API avec les options spécifiées
  fetch(url, fetchOptions)
    .then((response) => {
      // lorsque la réponse est reçue
      return response.json(); // convertit la réponse en objet JSON
    })
    .then((dataJSON) => {
      // lorsque l'objet JSON est disponible
      console.log(dataJSON); // affiche l'objet JSON dans la console
      getLivres(); // recharge la liste des livres à partir de l'API
    })
    .catch((error) => console.log(error)); // en cas d'erreur, affiche l'erreur dans la console
}

// -- handler pour diminuer la quantité de stock d'un livre à partir de son id
function handlerDiminuer(livre) {
  livre.diminuer();
  if (livre.qtestock === 0) {
    handlerDelete(livre.id);
  }
  console.log({ ...livre });
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/3/livres";
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({
      id: livre.id,
      titre: livre.titre,
      prix: livre.prix,
      qtestock: livre.qtestock,
    }),
  };
  // -- l'id du livre à modifier doit être
  //  ajouté à la fin de l'url
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getLivres();
    })
    .catch((error) => console.log(error));
}

// -- appel de la fonction defineExpose pour exposer les propriétés handlerAugmenter et handlerDiminuer
defineExpose({ handlerAugmenter, handlerDiminuer });
</script>
<style>
/* Je n'ai pas utilisé scoped car je voulais que le code CSS soit appliqué au body de tote la page*/
body {
  background-image: url("https://th.bing.com/th/id/R.c7ef8e376329f33ec771d1b00510a8cd?rik=QNMhfowptDOPTQ&riu=http%3a%2f%2fp9.storage.canalblog.com%2f95%2f30%2f1287745%2f101217223_o.jpg&ehk=3pXuptuT%2fK6P7gCC7FD7qyyDyWqWXAoWs1WPiShkPY0%3d&risl=&pid=ImgRaw&r=0");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  background-attachment: fixed;
}
</style>