<template>
  <div>
    <main class="px-5 bg-center pt-20 pb-10">
      <div class="flex lg:flex-row justify-between flex-col wrapper lg:items-center">
        <div class="mb-4 flex-col md:px-8 lg:px-0 lg:w-7/12 lg:text-left text-center">
          <h1 class="text-6xl font-bold text-gray-600">Blog posts</h1>
          <p class="mt-4 lg:mt-2 text-2xl text-gray-400">Check out our latest publications</p>
        </div>
        <div class="w-full px-3">
          <form class="m-auto mt-4 lg:m-0 lg:mt-0 lg:min-w-max" id="simple-search" @submit.prevent="filteredPosts" >
            <div class="relative w-full">
                <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                    <svg aria-hidden="true" v-on:click="test1" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path></svg>
                </div>
                <input v-model="filteredData" type="text" class="bg-gray-50 border py-4 border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-10 p-2.5  dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Look for interesting Posts">
            </div>
          </form>  
        </div>
      </div>
    </main>
      <div
        class="wrapper grid grid-cols-1 gap-y-6 px-6 lg:grid-cols-2 lg:gap-x-5 lg:gap-y-9"
      >
        <!-- Vue Loop for different Blog Posts -->
        <section
          v-for="post in filteredPosts"
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
                :src="getImageUrl(post.image)"
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
  </div>
</template>

<script>
import InkreaseSearch  from '../components/InkreaseSearch.vue'

export default {
  name: 'Blog',
  data(){
    return {
      postsObject: [
        {
          title: "Introducing Colombia - Diana Gabaldon",
          summary:
            "Twangs powerful low-code developer platform enables businesses to create high",
          date: "January 6, 2021",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post1",
          alt: "Description of the specific image",
        },
        {
          title: "Travel invention - Giving Voice to Every Business",
          summary:
            "Twangs Amazing low-code developer platform enables businesses to create high",
          date: "July 6, 2023",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post1",
          alt: "Description of the specific image",
        },
        {
          title: "Disney Intervention - Giving Voice to Every Business",
          summary:
            "Twangs SuperCool low-code developer platform enables businesses to create high",
          date: "March 6, 2024",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post1",
          alt: "Description of the specific image",
        },
        {
          title: "Outlander Stories 2022 - Diana Gabaldon",
          summary:
            "Twangs incredible low-code developer platform enables businesses to create high",
          date: "February 6, 2025",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post2",
          alt: "Description of the specific image",
        },
        {
          title: "Xperience Design - Giving Voice to Every Business",
          summary:
            "Sprout powerful low-code developer platform enables businesses to create high",
          date: "September 6, 2016",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post2",
          alt: "Description of the specific image",
        },
        {
          title: "1969 - Giving Voice to Every Business",
          summary:
            "Twangs powerful low-code developer platform enables businesses to create high",
          date: "August 6, 2014",
          author: "Limor Lahiani (PhD.), Navot Volk",
          image: "post2",
          alt: "Description of the specific image",
        },
      ],
      filteredData: ""
    }
  },
  components: {
    InkreaseSearch,
  },
  methods: {
    getImageUrl(path) {
    const url = `${path}.svg`;
    const imgUrl = new URL(url, import.meta.url).href;
    console.log(imgUrl)
    return imgUrl;
    }
  },
  computed: {
    filteredPosts() {
      return this.postsObject.filter((post) => {
        return post.title.toLowerCase().indexOf(this.filteredData.toLowerCase()) != -1;
      })

    }
  },  
}
</script>