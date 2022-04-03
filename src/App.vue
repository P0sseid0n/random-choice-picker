<script setup lang="ts">
import Choice from '@/components/Choice.vue'
import { ref, watch } from 'vue'

const choices = ref([] as { value: string, picked: boolean }[])
const choiceText = ref('')

watch(choiceText, () => {
   choices.value = choiceText.value.split(',').map(s => s.trim()).filter(s => s).map(v => ({ value: v, picked: false }))
})

function pick() {
   choices.value.forEach(c => c.picked = false)

   const index = Math.floor(Math.random() * choices.value.length)

   choices.value[index].picked = true
}

</script>

<template>
   <header>
      <h3>Use virgula (,) para separar as escolhas.</h3>
      <h3>Pressione enter para sortear</h3>
   </header>
   <main>
      <textarea
         v-model="choiceText"
         placeholder="Digite as escolhas aqui..."
         @keypress.enter.prevent="pick"
      ></textarea>
   </main>
   <footer>
      <Choice v-for="choice in choices" :choice="choice" />
   </footer>
</template>

<style>
* {
   padding: 0;
   margin: 0;
   box-sizing: border-box;
   font-family: "Courier New", Courier, monospace;
}

h3 {
   color: white;
}

header,
main,
footer {
   width: 100%;
   max-width: 480px;
}

header {
   text-align: center;
}

textarea {
   width: 100%;
   resize: vertical;
   min-height: 40px;
   max-height: 320px;
   padding: 8px;
   font-size: 16px;
   margin: 16px 0;
}

#app {
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;

   height: 100vh;
   background-color: #2b88f0;
}

footer {
   display: flex;
   flex-wrap: wrap;
   gap: 8px;
}
</style>
