<template>
  <div class="Sunrise-Sunset">
    <div class="form-container" v-show="showForm">
    <h1>Sunrise-Sunset</h1>
   
  

    <form v-on:submit.prevent="city">
    <p>Enter city name: <input type="text" v-model="query" placeholder="Seattle, WA"> <button type="submit">Search</button></p>
    
      </form>

      <spinner v-if = "showSpinner"></spinner>
    <ul v-if="results > 0" class="results">
      
     <li v-for="(city) in results" :key="city">
        <h2>{{ city.name }}, {{ city.sys.country }}</h2>
      
      </li>
    </ul>

    </div>
  </div>
</template>

<script>
 import axios from "axios";
 import Cubespinner from '@/views/Cubespinner';
export default {
  name: 'City',
  components: {
    spinner: Cubespinner
  },
  data() {
    return {
       results: null,
      query: '',
      showForm: true,
      showError: false,
      errors: null,
      showSpinner: false
    };
  },
   methods: {
 
    
    city: function () {
      this.results = null;
      this.showLoading = true;
      this.showSpinner = true
     
     console.log ()
     
      axios.get("https://api.sunrise-sunset.org/json", {
        
        params: {
         lat: 36.7201600,
         lng: -4.4203400
        }
        }
        )
 .then(response => {
          this.showSpinner = false;
          this.results = response.data;
           console.log (this.results.city);
         
       
        })
        .catch(error => {
      this.showSpinner = false;
        this.messages.push({
          type: 'error',
          text: error.message
         
          });
         
        })
    }
      }
    };
  
 
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