<template>
  <div id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>
    <div v-for="blog in filteredBlogs" class="single-blog">
       
       <router-link v-bind:to="'/blog/'+ blog.id"><h2>{{ blog.title | to-uppercase}}</h2></router-link> 
        <article>{{ blog.content| snippet }}</article>

    </div>
  </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin'

export default {

  data() {
    return {
        blogs: [],
        search:''
    }
  },

    created() {
    this.$http.get('https://posting-firebase-ed-1-default-rtdb.firebaseio.com/posts.json').then(function(data){
        return data.json();
    }).then(function(data){
      var blogsArray = []
      for (let key in data){
           data[key].id = key
           blogsArray.push(data[key])
      }
      this.blogs = blogsArray;
    });  
    },

    computed: {
     
    },
    mixins: [searchMixin]
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>
