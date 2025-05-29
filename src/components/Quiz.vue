<script setup>
import {computed, ref} from "vue";
import ProgressBar from "./ProgressBar.vue";
import Question from "./Question.vue";

// -Définition des props (propriétés) reçues par le composant
// Ici, on attend un objet 'quizData' contenant les données du quiz
const props = defineProps({
  quizData: Object // Type validation: indique que quizData doit être un Object
})

const answers = ref(props.quizData.questions.map(() => null))
const step = ref(0);

const questionQuiz = computed(() => props.quizData.questions[step.value])

const addAnswer = (answer) => {
  answers.value[step.value] =answer;
  step.value++
}
</script>

<template>
  <!-- -Template principal du composant -->
  <div>
    <!-- Affichage du titre du quiz récupéré depuis les props -->
   <h1 class="text-2xl text-green-700">
    {{ quizData.title }}
  </h1>
  <ProgressBar  :value="step" :max="quizData.questions.length - 1"/>
  <Question :questionQuiz="questionQuiz"  v-if="questionQuiz" @answer="addAnswer"/>
{{ answers}}

  </div>
</template>

<style scoped>
/* 
  Styles CSS scopés au composant seulement 
  (n'affecte pas les autres composants)
  Actuellement vide mais prêt à accueillir des styles spécifiques
*/
</style>
