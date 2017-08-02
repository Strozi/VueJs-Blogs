<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted">
      <label>Blog Title: </label>
      <input type="text" v-model.lazy="blog.title" required/>
      <label>Blog Content: </label>
      <textarea v-model.lazy="blog.content"></textarea>
      <div id="checkboxes">
        <label>Sport</label>
        <input type="checkbox" value="sport" v-model="blog.categories" />
        <label>Games</label>
        <input type="checkbox" value="games" v-model="blog.categories" />
        <label>Tech</label>
        <input type="checkbox" value="tech" v-model="blog.categories" />
        <label>Fashion</label>
        <input type="checkbox" value="fashion" v-model="blog.categories" />
      </div>
      <label>Author: </label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button v-on:click.prevent="post">Submit</button>
    </form>
    <div v-if="!submitted">
      <h3>Thanks for submitting a new Blog</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog title:{{blog.title}}</p>
      <p>Blog content:</p>
      <p>{{blog.content}}</p>
      <p>Blog author: {{blog.author}}</p>
      <p>Blog categories: </p>
      <ul>
        <li v-for="category in blog.categories" >
              {{category}}
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
export default {

  data () {
    return {
      blog:{
        title: "",
        content: "",
        author:"",
        categories: []
      },
      authors: ["Mateusz Borek","Pawe Opydo","Tomasz Jacykow"],
      submitted: false
    }
  },
  methods:{
    post:function(){
      this.$http.post('https://jsonplaceholder.typicode.com/posts', {
        title:this.blog.title,
        body: this.blog.content,
        userID: 102
      }).then(function(data){
          this.submitted=true;
      });
    }
  }

}
</script>

<style>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#checkboxes input{
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label{
  display: inline-block;
}
</style>
