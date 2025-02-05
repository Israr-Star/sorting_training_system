<template>
  <div class="flex items-center justify-between">
    <!-- Left Section: Title -->
    <h1 class="text-4xl font-bold leading-[37.5px] text-left text-[#555555]">
      Sorting Training System
    </h1>

    <!-- Middle Section: Timer -->
    <h1
      v-if="timer > 0 && civilServants?.length"
      class="text-[20px] font-bold leading-[22px] text-left text-[#555555]"
    >
      Your Time Started
      {{ Math.floor(timer / 3600) }} H : {{ Math.floor((timer % 3600) / 60) }} M
      : {{ timer % 60 }} S
    </h1>

    <!-- Right Section: Start Sorting Button -->
    <button
      class="w-[161px] h-[50px] rounded-[5px] bg-[#FF8D00] text-white cursor-pointer"
      @click="toggleModal"
    >
      Start Sorting
    </button>
  </div>
</template>

<script setup>
// Define props
const props = defineProps({
  timer: {
    type: Number,
    required: true,
  },
  civilServants: {
    type: Array,
    default: () => [],
  },
})

// Emit events
const emit = defineEmits(['start-sorting'])

// Method to handle button click
const toggleModal = () => {
  emit('start-sorting')
}
</script>

