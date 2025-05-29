<script setup>
// -Import des composants et fonctions nécessaires
import Enfant from "./components/Enfant.vue";
import Quiz from "./components/Quiz.vue"; // Import du composant Quiz
import { onMounted, ref } from "vue"; // Import des fonctions de composition Vue

// -Déclaration des états réactifs
const quizData = ref(null); // Stocke les données du quiz (null initialement)
const state = ref("loading"); // Gère l'état du composant ("loading", "idle" ou "erreur")

// -Hook de cycle de vie : exécuté après le montage du composant
onMounted(async () => {
  try {
    // 1. -Tentative de récupération des données du quiz
    const response = await fetch("/quiz.json");
    
    // 2. -Vérification si la réponse est OK (statut 200-299)
    if (!response.ok) {
      throw new Error("Erreur lors du chargement du quiz");
    }
    
    // 3. -Conversion de la réponse en JSON
    const data = await response.json();
    
    // 4. -Mise à jour des états
    quizData.value = data; // Stockage des données du quiz
    state.value = "idle";  // Passage en état "idle" (prêt)
    
  } catch (error) {
    // 5. -Gestion des erreurs
    console.error("Erreur:", error); // Log de l'erreur
    state.value = "erreur"; // Passage en état d'erreur
  }
});

const subTitre ='Développeur'
</script>

<template>
  <div class="container" style="margin-top:2rem">
    <!-- -Affichage conditionnel basé sur l'état -->
    
    <!-- 1. Cas d'erreur -->
    <div v-if="state === 'erreur'" class="error">
      Impossible de charger le quiz
    </div>
    
    <!-- 2. Cas où les données sont disponibles -->
    <div v-else-if="quizData">
      <!-- Affichage du composant Quiz avec passage des données -->
      <Quiz :quizData="quizData" v-if="quizData" />
    </div>
    
    <!-- 3. Cas de chargement (état par défaut) -->
    <div v-else>Chargement..</div>
  </div>

  <Enfant  :sub-titre="subTitre"/>
</template>
