<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>

      <div class="mt-2 mb-8 flex justify-center items-center">
        <img
          v-for="present in presentsSorted"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>

      <div class="w-full flex justify-center">
        <button class="bg-black text-white font-semibold rounded-lg px-6 py-3" @click="toggleSort">Toggle sort</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import presents from './presents.json'

let isSortedBySize = ref(false)

const sortBySize = (a, b) => a.dimensions.width * a.dimensions.height - b.dimensions.width * b.dimensions.height

const presentsSorted = computed(() => (isSortedBySize.value ? [...presents].sort(sortBySize) : presents))

const toggleSort = () => (isSortedBySize.value = !isSortedBySize.value)
</script>
