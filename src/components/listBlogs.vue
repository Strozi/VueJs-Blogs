<template>
  <div id="show-blogs">
    <h1>List Blog Titles</h1>
    <input type="text" v-model="search" placeholder="search blogs"/>
    <div v-for="blog in filteredBlogs " class="single-blog">
        <h2>{{blog.title |to-uppercase}}</h2>
        <article>
          {{blog.body |snippet}}
        </article>
    </div>
  </div>
</template>



<script>
import searchMixin from '../mixins/searchMixin';

export default {
  data () {
    return {
      blogs: [],
      search:''
    }
  },
  methods:{

  },
  created(){
    this.$http.get('firebase/posts/').then(function(data){

    })
  },
  computed:{


  },
  filters:{
    'to-uppercase': function(value){
      return value.toUpperCase();
    },
    'snippet': function(value){
      return value.slice(0,100) + '...';
    }
  },
  directives:{
    'rainbow': {
      bind(el,binding,vnode){
        el.style.color = "#" + Math.random().toString().slice(2,8);
      }
    }
  },
  mixins:[searchMixin]

}
</script>

<style>
  #show-blogs{
    max-width: 800px;
    margin: 0 auto;
  }
  .single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
  }
</style>
