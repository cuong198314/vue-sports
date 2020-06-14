<template>
  <div class="Sunrise-Sunset">
    <h1>Sunrise-Sunset</h1>
   
  

    <form v-on:submit.prevent="findCity">
    <p>Enter city name: <input type="text" v-model="query" placeholder="Seattle, WA"> <button type="submit">Go</button></p>
    
      </form>

       <load-spinner v-if="showLoading"></load-spinner>
    <ul class="cities" v-if="results && results.list.length > 0">
     <li v-for="(city,index) in results.list" :key="index">
        <h2>{{ city.name }}, {{ city.sys.country }}</h2>
        

       

        <p><button class="save" v-on:click="saveCity(city)">Save City to Favorites</button></p>
      </li>
    </ul>

   
  </div>
</template>

<script>

export default {
  name: 'Search',

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

    
    getCity: function () {
      this.showSpinner = true
 
     console.log ()
     
      
     .get("https://api.sunrise-sunset.org/json?lat=36.7201600&lng=-4.4203400&date=today", {
        
        params: {
         lat: '36.7201600&lng=-4.4203400'
        }
        }
        )
        .then(response => {
         
          this.results = response.data;
          this.showLoading = false;
        })
        .catch(error => {
          this.messages.push({
            type: 'error',
            text: error.message
          });
         
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