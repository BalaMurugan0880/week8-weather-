<template>
  <div id="search" class="container">
    <div class="row justify-content-md-center g-3 py-3">
      <h2>Weather Website</h2>
       <div class="col col-lg-2">
 
     </div>
      <div class="col-md-auto">
         <input type="text" v-model="cityName" class="form-control" name="city" placeholder="Enter City"> 
       </div>
       <div class="col-md-auto">
        <button class="btn btn-primary" v-on:click="fetchWeather">Search</button>
       </div>
       <div class="col col-lg-2">
     
    </div>
    </div>
    <div class="row justify-content-md-center g-3 py-3">
      <div class="card">
        <table class="table table-bordered">
                  
        <thead>
           <tr>
            <th>Date</th>
            <th>Weather</th>
            <th>Temperature</th>
            <th>Icon</th>
           </tr>
          </thead>

         <tbody id="weatherResult">
            <tr v-for="weather in weathers" :key="weather.id" v-on:click="selectWeather(weather)" >
              <td>{{ weather.dt }}</td>
              <td>{{ weather.weather[0].main }}</td>
              <td>{{ (weather.temp.day - 273.15).toFixed(2) }} &deg; C</td>
              <td><img v-bind:src="'http://openweathermap.org/img/w/' + weather.weather[0].icon + '.png' "></td>
            </tr>
                      
         </tbody>
             
        </table>
        
      </div>
    </div>
    <div class="row">
      <div class="card" v-if="selectedWeather">
        <p>{{ new Date(selectedWeather.dt*1000) }}</p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      //THis is how u create a variable
      cityName:"",
      resultCity:"",
      weathers:[],
      selectedWeather:null,

    }
  },
  methods: {

    selectWeather: function(weather){
      this.selectedWeather = weather;
    },
    fetchWeather:function(){
      let url = 'https://api.openweathermap.org/data/2.5/forecast/daily?q='+this.cityName+'&appid=9fd7a449d055dba26a982a3220f32aa2';
        fetch(url)
        .then((response) => response.json())
        .then(json => {
          // Do something with the data
          console.log(json);
          this.weathers = json.list


        });

    }

  }

};
</script>

<style>
#search {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
