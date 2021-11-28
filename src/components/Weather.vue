<template>
    <div id="wrapper" :class="(typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' :'')">
     <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar form-control"
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
           >
      </div>

      <div class="weather-wrap" v-if="(typeof weather.main != 'undefined')">

        <div class="location-box">
          <!-- country or city name and country code -->
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateFormatter() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <!-- temperature condition -->
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>

      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Weather',
    props: {
    // msg: String
  },

  data(){
     return{
          api_key: 'b73d6cafea04aa33d16fc26d63447873',
          base_url: 'https://api.openweathermap.org/data/2.5/',
          query: '',
          weather: {}
     }
  },

  methods: {
    fetchWeather(e){
        if(e.key == "Enter"){
          //  fetch data from base url
          fetch(`${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
             return res.json();
          })
          .then(this.setResults);
        }
    },

    setResults(results){
         this.weather = results;
    },

    dateFormatter(){
         let date = new Date();
         let months = ["January","February","March","April","May","June","July","August","September","October","November","December"];
         let days = ["Sunday","Saturday","Friday","Thursday","Wednesday","Tuesday","Monday"];
         let day = days[date.getDay()];
         let currentDay = date.getDate();
         let month = months[date.getMonth()];
         let year = date.getFullYear();

         return `${day} ${currentDay}, ${month} ${year}`;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* template styling */
   #wrapper{
        background-image: url('../assets/cloud-blue-sky.jpg');
        background-size: cover;
        background-position: bottom;
        transition: 0.4s;
   }
   main{
     min-height: 100vh;
     padding: 25px;
     background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

/* temperature wise background image change */
#wrapper.warm{
    background-image: url('../assets/cloud-warm.jpg');
}

/* search box styling */
 .search-box{
      width: 100%;
      margin-bottom:  30px;
 }
 .search-box .search-bar{
     display: block;
     width: 100%;
     padding: 15px;
     columns: #3333;
     font-size: 20px;
     border: none;
     appearance: none;
     outline: none;
     background: none;
     background-color: rgba(255, 255, 255, 0.5);
     border-radius: 0px 16px 0px 16px;
     transition: 0.4s;
 }

 .search-box .search-bar:focus{
      box-shadow: 0px 0px 16px rgba(255, 255, 255, 0.25);
      background-color:  rgba(255, 255, 255, 0.75);
      border-radius: 0px 16px 0px 16px;
 }

 /* weather info box styling */
 .location-box .location{
        color: #fff;
        font-size: 35px;
        font-weight: 500;
        text-align: center;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
 }
 .location-box .date{
        color: #fff;
        font-size: 24px;
        font-weight: 300;
        text-align: center;
        font-style: italic;
 }
.weather-box{
    text-align: center;
}

.weather-box .temp{
      display: inline-block;
      padding: 10px 25px;
      color: #fff;
      font-size: 108px;
      font-weight: 900;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.25);
      border-radius: 16px;
      margin: 30px 0px;
      box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather{
     color: #fff;
        font-size: 44px;
        font-weight: 700;
        text-align: center;
        font-style: italic; 
        text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
