<script setup>
import { onMounted } from 'vue'
import { initFlowbite } from 'flowbite'

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite()
})
</script>
<template>
  <div class="">
    <figure
      class="relative max-w-full transition-all duration-300 cursor-pointer filter grayscale hover:grayscale-0"
    >
      <a href="#">
        <img
          class="rounded-none"
          src="https://images7.alphacoders.com/633/633262.png"
          alt="image description"
        />
      </a>
      
    </figure>
  </div>
</template>
