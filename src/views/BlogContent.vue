<template>
  <div id="blog-content">
    <section class="bg-purple-900 bgHome py-28 sm:py-36 mb-9">
      <div class="wrapper px-5">
        <h1 class=" text-4xl sm:text-5xl text-white mb-4 font-bold">{{postContent.data.title}}</h1>
        <h6 class=" text-lg sm:text-2xl text-purple-300">Author: {{postContent.data.author.first_name}} {{postContent.data.author.last_name}}</h6>
        <h6 class=" text-sm sm:text-lg text-purple-400">Updated: {{getDate(postContent.data.updated)}}</h6>
      </div>
    </section>
    <figure class="wrapper px-5">
      <img :src="postContent.data.featured_image"  class="rounded-3xl h-30 md:h-[400px] w-full object-cover mb-4 -mt-28 sm:-mt-40" alt="">
    </figure>

      <div class="wrapper px-5" v-html="postContent.data.body"></div>
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
      console.log(res)
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