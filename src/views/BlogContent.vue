<template>
  <div id="blog-content">
    <h1>hghghg</h1>
    <section class="wrapper">
      <h1>{{postContent.data.title}}</h1>
      <div v-html="postContent.data.body"></div>
    </section>
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
  }
},
created() {
  this.getPost()
}
}
</script>