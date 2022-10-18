<template>
  <div
    class="grid grid-cols-1 gap-y-6 px-6 lg:grid-cols-2 lg:gap-x-5 lg:gap-y-9"
  >
    <!-- Vue Loop for different Blog Posts -->
    <section
      v-for="post in blogExports"
      :key="post.title"
      class="
        lg:mx-0
        border-2
        py-3
        px-3
        cursor-pointer
        rounded-xl
        hover:bg-slate-50
        gap
      "
    >
      <!-- Each Article -->
      <article class="lg:flex-row gap-5 flex flex-col">
        <figure class="rounded-xl overflow-hidden">
          <img
            :src="post.image"
            class="
              w-full
              h-full
              object-cover
              hover:scale-125
              transition-all
              duration-300
            "
            :alt="post.alt"
          />
        </figure>
        <div>
          <h2 class="font-bold text-3xl mb-4 hover:underline">
            {{ post.title }}
          </h2>
          <p>{{ post.summary }}</p>
          <div class="text-gray-500 mt-3">
            <p>{{ post.author }}</p>
            <p>{{ post.date }}</p>
          </div>
          <div class="mt-5 flex items-center gap-2">
            <a class="text-purple-700 font-semibold hover:underline" href="#"
              >Read More</a
            >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="13"
              height="8"
              viewBox="0 0 13 8"
              fill="none"
            >
              <path
                d="M1 4H11M11 4L8 1M11 4L8 7"
                stroke="#962EFF"
                stroke-width="2"
                stroke-linecap="round"
              ></path>
            </svg>
          </div>
        </div>
      </article>
    </section>
  </div>
</template>
<script>
export default {
  data() {
    return {
    }
  },
  props: {
    blogExports:null
  }
};
</script>
<style is:global>
</style>
