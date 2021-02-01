<template>

  <div class="container" id="app">
    <h1>{{ msg }}</h1>

    <br>
    <div class="center">
    <form action class="form center">
      <div class="row">
        <div class="col-md-6">
          <input class="form-control" required id="input-search" type="text" v-model="textSearch" v-on:change="logStuff()" placeholder='Buscar por Nombre...'>
        </div>
        <br>
      </div>
    </form>
  </div>
<br>
<br>
<div class="row" id="listaproyectos" >
      <div class="col-4" v-for="post in peopleFilter" :key="post">

        <b-card border-variant="dark"
        header="info"
        header-bg-variant="info"
        header-text-variant="white"
        align="center" title="Title" header-tag="header" footer-tag="footer">
              <template #header>
                <h6 class="mb-0">{{post.name}}</h6>
              </template>
              <b-card-text>Edad: <strong> {{post.age}}</strong></b-card-text>
              <b-card-text>Género: <strong>{{post.gender}}</strong></b-card-text>
              <b-card-text>Color de ojos: <strong>{{post.eye_color}}</strong></b-card-text>
              <b-card-text>Color de cabello: <strong>{{post.hair_color}}</strong></b-card-text>

            </b-card>
            <br>

      </div>
    </div>
    <div class="col-md-offset-4" id="Archivo">
      <input type="file" accept="image/*" @change="uploadImage($event)" id="file-input">
    </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data (){
    return{
      posts: [],
      lists: [],
      textSearch: "",
      textSearchAge: ""
    }
  },

  methods: {
    getData: function () {
      let card = this;
        axios.get('https://ghibliapi.herokuapp.com/people')
          .then(function(response) {
            card.posts = response.data;
        }).catch(error => {
              console.log(error);
        });
    },
    uploadImage(event) {

    const URL = 'http://foobar.com/upload';

    let data = new FormData();
    data.append('name', 'my-picture');
    data.append('file', event.target.files[0]);

    let config = {
      header : {
        'Content-Type' : 'image/png'
      }
    }

    axios.put(
      URL,
      data,
      config
    ).then(
      response => {
        console.log('image upload response > ', response)
      }
    )
  }
},
  mounted(){

    let vue = this;
    axios.get('https://ghibliapi.herokuapp.com/people').then( function (response) {
      vue.posts = response.data;
      console.log(vue.posts)
      console.log()
    })
    if(localStorage.textSearch){
      this.textSearch = localStorage.textSearch;
    }
  },

watch:{
  textSearch(newTextSearch){
    localStorage.textSearch = newTextSearch;
  }
},
  computed: {
    peopleFilter: function() {
      var textSearch = this.textSearch;
      return this.posts.filter(function(el) {
        return el.name.toLowerCase().indexOf(textSearch.toLowerCase()) !== -1 ;

      });
    }
 }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#Archivo{
  float: right;
  margin-top: 2%;
}
</style>
