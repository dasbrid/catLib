<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <button color="blue" large @click="loadNextImage" >load</button>
                    Another <v-icon>refresh</v-icon>

<div>
                    <img :src="image.url">
                    <img>
</div>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
import axios from "axios" // for calling APIs
export default {
    name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      image: { url: ""}
    }
  },
  mounted() {
    this.loadNextImage();
  },
  methods: {
    loadNextImage()
    {
        try{
            axios.defaults.headers.common['x-api-key'] = "DEMO-API-KEY" // Replace this with your API Key
            // let response = axios.get('https://api.thecatapi.com/v1/images/search', { params: { limit:1, size:"full" } } ) // Ask for 1 Image, at full resolution
            axios.get('https://api.thecatapi.com/v1/images/search', { params: { limit:1, size:"full" } } ) // Ask for 1 Image, at full resolution
            .then(response => {
              // eslint-disable-next-line
              console.log(response);
              this.image = response.data[0]
            })
            .catch(error=> {
              // eslint-disable-next-line
              console.log(error);
            })
            // this.image = response.data[0] // the response is an Array, so just use the first item as the Image
            // eslint-disable-next-line
            console.log("-- Image from TheCatAPI.com")
            // eslint-disable-next-line
            // console.log(response.data)
            //console.log("id:", this.image.id)
            
            // eslint-disable-next-line
            //console.log("url:", this.image.url)
        }catch(err){
          // eslint-disable-next-line
            //console.log(err)
        }
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
</style>
