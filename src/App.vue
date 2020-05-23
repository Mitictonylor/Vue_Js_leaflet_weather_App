<template lang="html">
  <div id="app" :class="typeof weather.main !='undefined' && chooseBackground()" >
    <main>
      <div class="search-box">
        <input class="search-bar" v-model="city" v-on:keypress="fetchTheWeather" type="text"  placeholder="Search..." />
        </div>
        <div>
      <weather-details v-if="typeof weather.main !='undefined'" :weather="weather"></weather-details>
      </div>
      <div>
        <vue-map v-if="typeof weather.main !='undefined'" :weather="weather"></vue-map>
      </div>
    </main>
  </div>
</template>

<script>
import WeatherDetails from './components/WeatherDetails.vue'
import VueMap from './components/Map.vue'
export default {
  name:'app',
  data(){
    return{
    key: '31423c45b9d32d686dff4fcd7e4aa4a0',
    url: "https://api.openweathermap.org/data/2.5/",
    city: '',
    weather:{}

  }},
  components:{
    'weather-details': WeatherDetails,
    'vue-map': VueMap
  },
  methods:{
    fetchTheWeather(event){
      if(event.key == "Enter"){
        fetch(`${this.url}weather?q=${this.city}&units=metric&APPID=${this.key}`)
        .then(res => res.json()).then(data => this.weather = data);
        this.city= ''

      }
    },
    chooseBackground: function(){
      if (this.weather.weather[0].main === "Rain"){
        return 'rain';
      } else if (this.weather.weather[0].main === "Clear"){
          return 'clear';
        } else if (this.weather.weather[0].main === "Clouds") {
          return 'clouds';
        } else if (this.weather.weather[0].main === "Haze") {
          return 'haze';
        }else if (this.weather.weather[0].main === "Mist") {
          return 'mist';
        }else
        return 'sunny';
  }
}
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: 'ComicSans', sans-serif;
}
#app{
  background-image: url('./assets/standard.gif');
/* riempe il background */
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  height: 800px;
  width: 500px
}
#app.clear {
  background-image: url('./assets/clear.gif');
}
#app.clouds {
  background-image: url('./assets/clouds.gif');
}
#app.haze {
  background-image: url('./assets/haze.gif');
}
#app.mist {
  background-image: url('./assets/mist.gif');
}
#app.rain {
  background-image: url('./assets/rain.gif');
}
#app.sunny {
  background-image: url('./assets/sunny.gif');
}
main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}
.search-box{
  width: 100%;
  margin-bottom: 30pxx;
}
.search-box .search-bar{
  display: block;
  width: 100%;
  /* grandezza campo */
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  /* toglie bordo esterno */
  border: none;
  /* toglie bordo quando selezionato */
  outline: none;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background: none;
  background-color: rgba(255,255,255, 0.5);
/* arrotonda i bordi altosx, adx,bassodx,bsx*/
  border-radius: 0px 15px 0px 15px;
transition: 0.4s
}
/* quando selezionato cambiamenti */
.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding: 5px 1px;
  color: #fff;
  font-size: 80px;
  font-weight: 900;
text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
background-color: rgba(255,255,255, 0.10);
border-radius: 30px;
margin: 30px 0px;
box-shadow: 3px 6px rgba(0,0, 0, 0.25);
}
.weather-box .real-feel{
  padding: 5px 1px;
  color: Green;
  font-size: 28px;
  font-weight: 400;
  font-style: normal;
  text-shadow: 2px 2px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255, 0.10);
  border-radius: 10px;
  margin: 5px 0px;
  box-shadow: 3px 6px rgba(0,0, 0, 0.25)
}
.weather-box .max{
  padding: 5px 1px;
  color: darkred;
  font-size: 28px;
  font-weight: 400;
  font-style: normal;
  text-shadow: 2px 2px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255, 0.10);
  border-radius: 10px;
  margin: 5px 0px;
  box-shadow: 3px 6px rgba(0,0, 0, 0.25)
}
.weather-box .min{

  padding: 5px 1px;
  color: darkblue;
  font-size: 28px;
  font-weight: 400;
  font-style: normal;
  text-shadow: 2px 2px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255, 0.10);
  border-radius: 10px;
  margin: 5px 0px;
  box-shadow: 3px 6px rgba(0,0, 0, 0.25)
}
.weather-box .weather{
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25)
}

</style>
