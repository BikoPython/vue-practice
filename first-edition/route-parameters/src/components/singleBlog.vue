<template>
    <div id="single-blog">
        <h1></h1>{{blog.title}}
        <article>{{blog.body}}</article>
    </div>  
</template>

<script>

export default {
    data() {
        return {
            id: this.$route.params.id,
            blog: {}
        }
    },
    created(){
        this.$http.get('https://jsonplaceholder.typicode.com/posts/' + this.id).then(function(data){
           
           this.blog = data.body; 
        });
    }
}
</script>
<style scoped>
#single-blog
{
    max-width: 960px;
    margin: 0 auto;
}
</style>