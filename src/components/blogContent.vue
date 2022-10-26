<template>
  <div v-for="post in PostContent" :key="post.title">
    <h2>{{post.title}}</h2>

  </div>
  
</template>
<script>
import Butter from 'buttercms';
const butter = Butter('c4132363d0ae8e6bdd024c99dc21de914f4b8cbd');

export default {
data()   {
  return {
    postContent: null
  }
},
methods: {
  getPost() {
    butter.post.retrieve(this.$route.params.slug)
    .then(res => {
      console.log(res)
      this.postContent = res.data
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