<template>
  <div id="blog-content">
    <section class="bg-purple-900 bgHome pb-24 pt-8 sm:py-24 sm:pb-40 mb-9">
      <div class="wrapper px-5">
          <!-- Breadcrumb -->
        <nav class="flex py-5 text-white" aria-label="Breadcrumb">
          <ol class="inline-flex items-center space-x-1 md:space-x-3">
            <li>
              <div class="flex items-center">
                <svg class="w-4 h-4 mr-2" fill="#A855F7" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"></path></svg>
                <router-link to="/blog" class="text-sm font-medium text-purple-500 hover:text-purple-400 md:ml-2">
                Blog
                </router-link>
              </div>
            </li>
            <li aria-current="page">
              <div class="flex items-center">
                <svg class="w-6 h-6 text-white" fill="white" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"></path></svg>
                <span class="ml-1 text-sm font-medium text-white md:ml-2">{{postContent.data.title}}</span>
              </div>
            </li>
          </ol>
        </nav>
        <h1 class=" text-4xl sm:text-5xl text-white mb-4 font-bold">{{postContent.data.title}}</h1>
        <h6 class=" text-lg sm:text-2xl text-purple-300">Author: {{postContent.data.author.first_name}} {{postContent.data.author.last_name}}</h6>
        <h6 class=" text-sm sm:text-lg text-purple-400">Updated: {{getDate(postContent.data.updated)}}</h6>
      </div>
    </section>
    <figure class="wrapper px-5">
      <img :src="postContent.data.featured_image"  class="rounded-3xl h-30 md:h-[400px] w-full object-cover mb-4 -mt-28 sm:-mt-40" alt="">
    </figure>
      <div class="single-post wrapper px-5" v-html="postContent.data.body"></div>
  </div>
</template>
<script>
import Butter from 'buttercms';
const butter = Butter('c4132363d0ae8e6bdd024c99dc21de914f4b8cbd');

export default {
name: 'blog-content',
data()   {
  return {
    postContent: {}
  }
},
methods: {
  getPost() {
    butter.post.retrieve(this.$route.params.slug)
    .then(res => {
      this.postContent = res.data
    }). catch( res =>{
      console.log(res)
    })
  },
  getDate(dateString) {
  const date = new Date(dateString);
  return new Intl.DateTimeFormat('default', {dateStyle: 'short'}).format(date);
  }
},
created() {
  this.getPost()
}
}
</script>

<style scoped>
:deep()h3 {
  font-weight: bold;
  font-size: 1.5rem;
  margin-block: 1em;
}

</style>