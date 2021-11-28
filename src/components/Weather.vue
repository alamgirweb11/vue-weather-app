<template>
    <div id="wrapper">
     <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar form-control"
          v-model="query"
          placeholder="Search...">
      </div>

      <div class="weather-wrap">

        <div class="location-box">
          <div class="location">Bangladesh</div>
          <div class="date">Monday 29 November 2021</div>
        </div>

        <div class="weather-box">
          <div class="temp">8°C</div>
          <div class="weather">Rain</div>
        </div>

      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Weather',
  data(){
     return{
          api_key: 'b73d6cafea04aa33d16fc26d63447873',
          base_url: 'https://api.openweathermap.org/data/2.5/',
          query: '',
          weather: {}
     }
  },
  props: {
    // msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
