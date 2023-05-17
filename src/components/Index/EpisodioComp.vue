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
          src="https://images7.alphacoders.com/106/1062176.jpg"
          alt="image description"
        />
      </a>
    
    </figure>
  </div>
  <div class="">
    <section
      class="m-9 bg-white dark:bg-gray-900 bg-[url('https://flowbite.s3.amazonaws.com/docs/jumbotron/hero-pattern.svg')] dark:bg-[url('https://flowbite.s3.amazonaws.com/docs/jumbotron/hero-pattern-dark.svg')]"
    >
      <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:py-19 z-10 relative">
        <h1
          class="mb-4 text-2xl sm:text-4xl font-extrabold tracking-tight leading-none text-gray-900 md:text-5xl lg:text-6xl dark:text-white"
        >
          Aqui encontraras todos los espisodios
        </h1>
        <p
          class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 lg:px-48 dark:text-gray-200"
        >
          estas listo para esta aventura
        </p>
      </div>
      <div
        class="bg-gradient-to-b from-blue-50 to-transparent dark:from-blue-900 absolute top-0 left-0 z-0"
      ></div>
    </section>
  </div>

  <div>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 p-9 mt-20">
      <div v-for="epi in epis" :key="epi.id">
        <a
          href="#"
          class="flex h-full flex-col items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700"
        >
          <img
            class="object-cover w-full h-full rounded-t-lg md:w-48 md:rounded-none md:rounded-l-lg"
            src="https://images5.alphacoders.com/728/728997.jpg"
            alt=""
          />
          <div class="flex flex-col justify-between p-4 leading-normal">
            <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
              <h2>Episodio</h2>
              {{ epi.episode }}
            </h5>
            <h2>Nombre:</h2>
            <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
              {{ epi.name }}
            </p>
            <h2>Fecha:</h2>
            <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
              {{ epi.air_date }}
            </p>
          </div>
        </a>
      </div>
    </div>
  </div>
  <div class="p-9 flex justify-center">
    <nav aria-label="Page navigation example">
      <ul class="inline-flex items-center -space-x-px">
        <li>
          <a
            @click="previousPage"
            :disabled="currentPage === 1"
            class="block cursor-pointer px-3 py-2 ml-0 leading-tight text-gray-500 bg-white border border-gray-300 rounded-l-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
          >
            <span class="sr-only">Previous</span>
            <svg
              aria-hidden="true"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </a>
        </li>
        <li>
          <a
            class="px-3 py-2 cursor-pointer leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
            >{{ currentPage }} de {{ totalPages }}</a
          >
        </li>
        <li>
          <a
            @click="nextPage"
            :disabled="currentPage === totalPages"
            class="block cursor-pointer px-3 py-2 leading-tight text-gray-500 bg-white border border-gray-300 rounded-r-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
          >
            <span class="sr-only">Next</span>
            <svg
              aria-hidden="true"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>
<script>
export default {
  data() {
    return {
      epis: [],
      currentPage: 1,
      // nameEpisodes: [],
      totalPages: 0,
      nameEpisode: ''
    }
  },
  mounted() {
    this.fetchEpisodes()
  },
  methods: {
    fetchEpisodes() {
      const api = import.meta.env.VITE_BASE_URL
      const apiEpisode = api + 'episode?page=' + this.currentPage

      fetch(apiEpisode)
        .then((response) => response.json())
        .then((data) => {
          this.epis = data.results
          this.totalPages = data.info.pages
          // this.items.forEach((e) => {
          //   let episode = e.episode[0]
          //   let apiEpisodes = episode
          //   fetch(apiEpisodes)
          //     .then((response) => response.json())
          //     .then((data) => {
          //       // console.log(data);
          //       this.nameEpisodes = data
          //       console.log(this.nameEpisodes)
          //       // console.log(this.nameEpisodes)
          //     })
          // })
        })
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--
        this.fetchEpisodes()
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++
        this.fetchEpisodes()
      }
    },
    getName(episode) {
      let apiEpisode = episode[0]
      fetch(apiEpisode)
        .then((response) => response.json())
        .then((data) => {
          this.nameEpisode = data.name
          console.log(this.nameEpisode)
        })
    }
  }
}
</script>
