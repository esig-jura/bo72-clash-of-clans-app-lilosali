<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {onMounted, ref} from "vue";

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes')//Appelle à l'API
      .then(function(reponseAPI) {return reponseAPI.json()})//on récupère les données en JSON et on les transforme en objet JAVA
      .then((donnesAuFormatJS) => { //ON récupère les données au format JavaScript
        troupes.value = donnesAuFormatJS //On les stocke dans la variable troupes
      })
})

// Tableau des troupes
const troupes = ref([])
</script>

<template>
  <page-top-barre :or="totalOr" />
  <body>
  <header>
    <h1>
      <img src="/img/clash-of-clans-logo.webp" alt="Logo Clash of Clans">
    </h1>
    <p class="description">
      Construire un village,
      former un clan et participer à des guerres de clans épiques !
    </p>
  </header>
  <main>
    <ul class="cartes">
      <li v-for="troupe in troupes" :key="troupe.id">
        <article>
          <header :style="'background: linear-gradient(60deg ,#3B3B3B 0% ,'+ troupe.couleur + ' 100%);'">
            <img :src="troupe.image"
                 :alt="troupe.nom">
          </header>
          <div class="level" :style="{color: troupe.couleur}">
            Niveau {{troupe.niveau}}
          </div>
          <h2 class="name">{{troupe.nom}}</h2>
          <button :style="{backgroundColor: troupe.couleur}"> Former
            <img src="/img/piece-or.png" alt="Former"></button>
          <p class="description">{{troupe.description}}</p>
          <footer>
            <div class="training"
                 :style="{backgroundColor: troupe.couleur}">
              <div>{{troupe.formation}}<sup>sec</sup></div>
              <div>Formation</div>
            </div>
            <div class="speed"
                 :style="{backgroundColor: troupe.couleur}">
              <div>{{troupe.vitesse}}</div>
              <div>Vitesse</div>
            </div>
            <div class="cost"
                 :style="{backgroundColor: troupe.couleur}">
              <div>{{troupe.cout}}</div>
              <div>Coût</div>
            </div>
          </footer>
        </article>
      </li>
    </ul>
  </main>
  <footer>
    &copy; 2023 - Supercell.com
  </footer>
  </body>
</template>

<style scoped lang="sass">

</style>