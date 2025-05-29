<script setup>
import { ref, computed } from 'vue';


const props = defineProps({
 questionQuiz: Object
})

const emits = defineEmits(['answer'])
const answer = ref(null)

const hasAnswer =computed(() => answer.value !== null)

</script>

<template>
 
 <div class="question">
  <h3>{{ questionQuiz.question }}</h3>
  <ul class="pl-12 list-none" >
    <li v-for="(choice, index) in questionQuiz.choices" :key="choice">
     <label :for="`answer${index}`">
      <input 
        :id="`answer${index}`"
        :value="choice"
        v-model="answer"
      type="radio" name="answer" />  {{ choice }}
     </label>
    </li>
  </ul>
<!-- {{ answer }} -->
  <button 
  :disabled="!hasAnswer"
  @click="emits('answer', answer)">Question suivante</button>

 </div>
</template>

<style scoped>

.question {
  padding-top: 2rem;
}
.question button{
  margin-left:auto;
  display:block;
}
</style>
