<script setup lang="ts">
import { defineProps } from 'vue'

defineProps<{ choice: { value: string, picked: boolean } }>()
</script>

<template>
   <span :class="{ 'picked': choice.picked }">{{ choice.value }}</span>
</template>



<style scoped>
span {
   border-radius: 8px;
   color: white;
   background: #f0932b;
   display: inline-block;
   font-weight: bold;

   padding: 4px 16px;
}

.picked {
   background: #273c75;
}
</style>