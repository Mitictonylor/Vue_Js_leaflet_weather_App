<template lang="html">
<div>
  <div class="weather-wrap" v-if="typeof weather.main !='undefined'">
    <div class="location-box">
      <div class="location">{{weather.name}},{{weather.sys.country}}</div>
      <div class="date">{{dateBuilder()}}</div>
    </div>
    <div class="weather-box">
      <div class="temp">{{Math.round(weather.main.temp)}}°c </div>
      <div class="weather">{{weather.weather[0].main}}</div>
      <div class="real-feel"> Feels like:{{Math.round(weather.main.feels_like)}}°c </div>
      <div class="max">Max: {{Math.round(weather.main.temp_max)}}°c</div>
      <div class="min">Min:{{Math.round(weather.main.temp_min)}}°c</div>

    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "WeatherDetails",
  props:['weather'],
  methods:{
    dateBuilder(){
      let d = new Date();
      let months = ['January', "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ['Sunday', "Monday", "Tuesday", "Wednesday","Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()]
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`
    },





    }

  }
</script>

<style lang="css" scoped>
</style>
