<template>
  <div id="app">
    <main>
      <div class="search-box">
        <h1>Mr Water</h1>
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
          >
          
      </div>

      <div  v-if="[typeof weather.main != 'undefined'] " class="weather-wrap">
        <div class="location-box">
          <div class="location"></div>
          <div class="date"></div>
        </div>
      </div>

      <div class="weather-box">
        <div class="temp">{{weather.current.temp_c}}° C</div>
        <div class="weather">{{weather.location.region}} - {{weather.location.name}}</div>
      </div>

    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_key:'4cc20ceba315426996f43152212712',
      url_base:'api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key === "Enter"){
        fetch(`http://api.weatherapi.com/v1/current.json?key=${this.api_key}&q=${this.query}&aqi=no`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results){
      this.weather = results;
      var parseobj = JSON.parse(JSON.stringify(this.weather));
      console.log(parseobj);
    }
  }
}
</script>

<style>

</style>
