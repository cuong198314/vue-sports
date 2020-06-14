<template>
  <div class="Sunrise-Sunset">
    <h1>Sunrise-Sunset</h1>
   
  

    <form v-on:submit.prevent="findCity">
    <p>Enter city name: <input type="text" v-model="query" placeholder="Seattle, WA"> <button type="submit">Go</button></p>
    
      </form>

       <load-spinner v-if="showLoading"></load-spinner>
    <ul class="cities" v-if="results && results.list.length > 0">
     <li v-for="(city) in results.list" :key="city">
        <h2>{{ city.name }}, {{ city.sys.country }}</h2>
        

       

        
      </li>
    </ul>

   
  </div>
</template>

<script>
 import axios from "axios";

export default {
  name: 'City',

  data() {
    return {
       results: null,
      query: '',
      showLoading: false,
      messages: [],
      favorites: []
    }
  },

   methods: {
 
    
    findCity: function () {
      this.showLoading = true
 
     console.log ()
     
      axios.get("https://api.sunrise-sunset.org/json", {
        
        params: {
         lat: '36.7201600',
         lng: '-4.4203400'
        }
        }
        )
 .then(response => {
          this.showLoading = false;
          this.results = response.data;
          console.log (this.results.findCity[0]);
       
        })
        .catch(error => {
       this.errors.push(error);
          });
         
        }
      }
    }
  
 

</script>
<style scoped>
.errors li {
  color: red;
  border: solid red 1px;
  padding: 5px;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  width: 300px;
  min-height: 300px;
  border: solid 1px #e8e8e8;
  padding: 10px;
  margin: 5px;
}
a {
  color: #42b983;
}
</style>
