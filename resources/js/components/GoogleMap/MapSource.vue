<template>
  <div>
    <div>
        <h2>Search and add a pin</h2>
        <label>
            <gmap-autocomplete
                @place_changed="setPlace">
            </gmap-autocomplete>
            <button @click="addMarker">Add</button>
        </label>
      <br/>

    </div>
    <br>
    <gmap-map
        :center="center"
        :zoom="12"
        style="width:100%;  height: 400px;"
    >
        <gmap-marker
            :key="index"
            v-for="(m, index) in markers"
            :position="m.position"
            @click="center=m.position"
        ></gmap-marker>
    </gmap-map>
  </div>
</template>

<script>

export default {
    name: 'google-maps',
    components: {
       // GmapMarker
    },
    data(){
        return {
            markers: [],
            center: { lat: 41.342, lng:69.211},
            markers: [],
            places: [],
            currentPlace: null
        }
    },
    mounted() {
        this.geolocate();
    },
    computed: {
        //
    },
    methods: {
        setPlace(place) {
           this.currentPlace = place;
        },
        addMarker() {
            if (this.currentPlace) {
                const marker = {
                    lat: this.currentPlace.geometry.location.lat(),
                    lng: this.currentPlace.geometry.location.lng()
                };
                this.markers.push({ position: marker });
                this.places.push(this.currentPlace);
                this.center = marker;
                this.currentPlace = null;
            }
        },
        geolocate: function() {
            navigator.geolocation.getCurrentPosition(position => {
                this.center = {
                    lat: position.coords.latitude,
                    lng: position.coords.longitude
                };
            });
        }
    }
}
</script>

<style scoped>

</style>