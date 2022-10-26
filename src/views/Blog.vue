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

        <section v-for="post in filteredPosts" :key="post.title" 
            class="lg:mx-0 border-2 py-3 px-3 cursor-pointer rounded-xl hover:bg-slate-50 mb-5">
          <!-- Each Article -->
          <router-link :to="'/blog/' + post.slug">
            <article class="sm:flex-row gap-5 flex flex-col h-full">
              <figure class="rounded-xl overflow-hidden sm:w-1/2">
                <img
                  :src="(post.featured_image)"
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
              <div class="sm:w-1/2 flex flex-col justify-between">
              <div>
                <h2 class="font-bold text-3xl mb-2 hover:underline">
                  {{ post.title }}
                </h2>
                <p class="elipsis-text">{{ post.summary }}</p>
                <div class="text-gray-500 mt-3 flex gap-3 items-center">
                  <img class="w-12" :src="(post.author.profile_image)" alt="">
                  <div>
                    <p class="text-sm">Author: {{ post.author.first_name}} {{ post.author.last_name}}</p>
                    <p class="text-xs">Updated: {{getDate(post.updated)}}</p>
                  </div>
                </div>
              </div>
              <div>
                <hr class="my-2">
                <div class="mt-2">
                  <div class="flex items-baseline gap-2 self-end float-right">
                    <a class="text-purple-700 font-semibold hover:underline" :href="(post.url)"
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
              </div>
              </div>
            </article>
          </router-link>
        </section>
      </div>
  </div>
</template>

<script>
import InkreaseSearch  from '../components/InkreaseSearch.vue'
import Butter from 'buttercms';
const butter = Butter('c4132363d0ae8e6bdd024c99dc21de914f4b8cbd');


export default {
  name: 'Blog',
  data(){
    return {
      postsObject: [],
      filteredData: ""
    }
  },
  components: {
    InkreaseSearch,
  },
  methods: {
    getDate(dateString) {
      const date = new Date(dateString);
      return new Intl.DateTimeFormat('default', {dateStyle: 'short'}).format(date);
    },
    getPosts(){
      butter.post.list({
        page: 1,
        page_size: 10,
      }).then(res => {
        console.log(res)
        this.postsObject = res.data.data
      })
    }
  },
  computed: {
    filteredPosts() {
      return this.postsObject.filter((post) => {
        return post.title.toLowerCase().indexOf(this.filteredData.toLowerCase()) != -1;
      })

    }
  },
  created() {
    this.getPosts()
  }
}
</script>

<style scoped>
.elipsis-text {
  width: 100%;
  display: inline-block;
  max-height: calc(1.4em * 3);
  overflow: hidden;
}

.elipsis-text:after {
  content:"...";
  bottom: 0;
  right: 0;
}
</style>