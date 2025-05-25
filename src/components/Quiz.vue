<script setup>
// Définition des props (propriétés) reçues par le composant
// Ici, on attend un objet 'quizData' contenant les données du quiz
defineProps({
  quizData: Object // Type validation: indique que quizData doit être un Object
})
</script>

<template>
  <!-- Template principal du composant -->
  <div>
    <!-- Affichage du titre du quiz récupéré depuis les props -->
    {{ quizData.title }}
  </div>
</template>

<style scoped>
/* 
  Styles CSS scopés au composant seulement 
  (n'affecte pas les autres composants)
  Actuellement vide mais prêt à accueillir des styles spécifiques
*/
</style>
