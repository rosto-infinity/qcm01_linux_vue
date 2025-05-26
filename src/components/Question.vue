<script setup>

const props = defineProps({
 questionQuiz: Object
})

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
      type="radio" name="answer" />  {{ choice }}
     </label>
    </li>
  </ul>

  <button>Question suivante</button>

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
