<template>
  <div>
    <section v-for="post in PostContent" :key="post.title">
      <h1>{{post.data.title}}</h1>
      <div v-html="post.data.body"></div>
    </section>
  </div>
</template>
<script>
import Butter from 'buttercms';
const butter = Butter('c4132363d0ae8e6bdd024c99dc21de914f4b8cbd');

export default {
name:'blog-content',
data()   {
  return {
    postContent: null
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