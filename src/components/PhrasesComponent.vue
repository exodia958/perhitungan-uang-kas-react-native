<script setup lang="ts">
import{ ref } from 'vue'
import { getOneQuote } from 'src/composables/useQuotes'

 const quote = ref(getOneQuote());

</script>

<template>
  <div>
    <h5 class="q-ma-none">Berkas Kekayaan</h5>
    <q-separator></q-separator>
    <h6 class="q-ma-none">{{ quote?.description }}</h6>
  </div>
</template>

<style scoped>

</style>
