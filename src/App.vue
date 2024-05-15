<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {onMounted, ref} from "vue";
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageHeader from "@/components/PageHeader.vue";
import PageFooter from "@/components/PageFooter.vue";
import TroupeCarte from "@/components/TroupeCarte.vue";

//Tableau
let totalOr = ref(100000);

//

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
  <PageTopBarre :or="totalOr"/>
  <PageHeader/>
  <ul class="cartes">
    <li v-for="trp in troupes" :key="trp.id">
      <troupe-carte
          :troupe="trp"
          :or="totalOr"
      />
    </li>
  </ul>

  <PageFooter/>

</template>

<style scoped lang="sass">

</style>