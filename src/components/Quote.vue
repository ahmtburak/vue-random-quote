<script>
export default {
  data() {
    return {
      imageUrl: '',
      quote: {
        content: '',
        author: ''
      }
    }
  },
  methods: {
    async getImage() {
      this.imageUrl = await fetch('https://source.unsplash.com/random/?motivation').then(
        (res) => res.url
      )
    },
    async fetchQuote() {
      const data = await fetch('https://api.quotable.io/random').then((res) => res.json())
      this.quote = {
        content: data.content,
        author: data.author
      }
    }
  },
  created() {
    this.fetchQuote()
  }
}
</script>
<template>
  <!--Container-->
  <div
    class="min-w-screen min-h-screen bg-cover bg-no-repeat bg-fixed bg-center flex items-center justify-center px-5 py-5"
    :style="[
      imageUrl
        ? { backgroundImage: `url(${imageUrl})` }
        : {
            backgroundImage: `url(https://images.unsplash.com/photo-1497561813398-8fcc7a37b567?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80)`
          }
    ]"
  >
    <!--Quote Section-->
    <div
      class="w-full mx-auto rounded-lg bg-white shadow-lg px-5 pt-5 pb-10 text-gray-800"
      style="max-width: 500px"
    >
      <div class="w-full pb-5"></div>
      <div class="w-full pb-4">
        <div class="text-3xl text-indigo-500 text-left leading-tight h-3">"</div>
        <!--Quote Text-->
        <p class="text-sm text-gray-600 text-center px-5">
          {{ quote.content }}
        </p>
        <div class="text-3xl text-indigo-500 text-right leading-tight h-3 mt-3">"</div>
      </div>
      <div class="w-full">
        <p class="text-md text-indigo-500 font-bold text-center">{{ quote.author }}</p>
      </div>
      <div class="w-full flex justify-center items-center">
        <div
          @click="
            fetchQuote();
            getImage();
          "
          class="mt-4 inline-flex justify-center items-center px-5 py-3 text-base font-medium text-center text-indigo-100 border border-indigo-500 rounded-lg shadow-sm cursor-pointer hover:text-white bg-gradient-to-br from-purple-500 via-indigo-500 to-indigo-500"
        >
          <svg
            class="w-5 h-5 mr-2"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13 10V3L4 14h7v7l9-11h-7z"
            ></path>
          </svg>
          <span class="relative">Generate Quote</span>
        </div>
      </div>
    </div>
  </div>
</template>
