<template lang="html">
  <div id="vue-map">
  </div>
</template>

<script>
import L from 'leaflet';

export default {
  name: 'vue-map',
  props: ["weather"],
  components: {

  },
  data() {
    return {
      city: "",
      zoom: 10,
      center: [this.weather.coord.lat, this.weather.coord.lon],
      url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    }
  },
  mounted(){
this.startTheMap()
  },
  methods: {
    addMarker(coords, message){
      L.marker(coords).addTo(this.map)
      .bindPopup(message)
    },
    startTheMap(){
    if (this.map != undefined) {
      this.map.remove(); }
      this.city = this.weather.name
      this.center =[this.weather.coord.lat, this.weather.coord.lon ]
      this.map = L.map('vue-map');
      this.map.addEventListener('click', (e) => {
        let coords = [e.latlng.lat, e.latlng.lng]
        this.addMarker(coords, `Lat: ${coords[0]}, Lng: ${coords[1]} `)
      });
      this.map.setView(this.center, this.zoom);
      L.tileLayer(this.url, {attribution: this.attribution}).addTo(this.map);
      this.addMarker([this.weather.coord.lat, this.weather.coord.lon], this.weather.name);
    }

  },
  watch:{
    weather: function(){
      this.startTheMap()
    }
  }
}
</script>

<style lang="css" scoped>
#vue-map {
	width:300px;
	height:300px;
  margin:0;
  padding:0
}
@import "~leaflet/dist/leaflet.css";
</style>
