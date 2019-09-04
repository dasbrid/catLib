<template>
<div class="hello">
    <h1>{{ msg }}</h1>
    <button color="blue" large @click="loadNextImage" >load</button>

<img :src="image.url"><img>
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
