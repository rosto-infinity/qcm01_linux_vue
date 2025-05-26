<script setup>

defineProps({
  value : Number,
  max: Number
})

</script>

<template>
  <div>
   Etape  {{ value +1  }} /{{ max + 1}}
   <progress :value="value" :max="max" />
  </div>

</template>

<style scoped>
</style>
