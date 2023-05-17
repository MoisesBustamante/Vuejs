<script setup>
import { onMounted } from 'vue'
import { initFlowbite } from 'flowbite'

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite()
})
</script>
<template>
  <div class="mb-2">
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
      <figcaption class="absolute px-4 text-lg text-white bottom-6">
        <p>Do you want to get notified when a new component is added to Flowbite?</p>
      </figcaption>
    </figure>
  </div>
</template>
