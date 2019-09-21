<template>
    <div class="">
        <label>
            <div class="form-group">
                <div class="input-group">
                    <GmapAutocomplete
                        @place_changed="setPlace"
                        class="form-control"
                        :value="markerSearch"
                    >
                    </GmapAutocomplete>
                    <div class="input-group-append">
                        <button class="btn btn-info" @click="addMarker">Add</button>
                    </div>
                </div>
            </div>
        </label>
        <br/>

        <GmapMap
            :center="{lat: 41.342, lng:69.211}"
            :zoom="14"
            :style="mapStyle"
        >
        <GmapMarker 
            :key="index" 
            v-for="(m, index) in markers" 
            ref="myMarker"
            :position="google && new google.maps.LatLng(m.markerLat, m.markerLng)"
            :title="m.title"
            :icon="m.iconOptions"
            :url="m.url"
            @click="markerClick(m)"
            @mouseenter="setStyleMarker(m)"
        />
        </GmapMap>
    </div>
</template>

<script>
import {gmapApi} from 'vue2-google-maps'
export default {
    data() {
        return {
            mapStyle: {
                height:'700px', 
                width: '100%'
            },
            markerSearch: null,
            markers: [
                {
                    markerLat: 41.3211968697085,
                    markerLng: 69.20623843029148,
                    title: 'Hello world',
                    url: 'https://maps.google.com/?cid=2950277614791969222',
                    stl: 'width:10px; height: 10px',
                    iconOptions: {
                        url:'../img/apteka.png',                    
                        size: {width: 60, height: 60, f: 'px', b: 'px',},
                        scaledSize: {width: 70, height: 70, f: 'px', b: 'px',},
                    }
                },
                {
                    markerLat: 41.341,
                    markerLng: 69.213,
                    iconOptions: {
                        url:'../img/apteka.png',                    
                        size: {width: 60, height: 60, f: 'px', b: 'px',},
                        scaledSize: {width: 70, height: 70, f: 'px', b: 'px',},
                    }
                },
                {
                    markerLat: 41.343,
                    markerLng: 69.214,
                    iconOptions: {
                        url:'../img/apteka.png',                    
                        size: {width: 60, height: 60, f: 'px', b: 'px',},
                        scaledSize: {width: 70, height: 70, f: 'px', b: 'px',},
                    }
                },
                {
                    markerLat: 41.344,
                    markerLng: 69.215,
                    iconOptions: {
                        url:'../img/apteka.png',                    
                        size: {width: 60, height: 60, f: 'px', b: 'px',},
                        scaledSize: {width: 70, height: 70, f: 'px', b: 'px',},
                    }
                },
            ],
            newMarker: '',
            currentPlace: null
        }
    },
    mounted(){
        // this.addMarker()
    },
    computed: {
        google: gmapApi
    },
    methods: {
        setPlace(place){
            this.currentPlace = place;
            // console.log(place)
        },
        addMarker(){
            var app = this.markers.push({
                markerLat:this.currentPlace.geometry.location.lat(), 
                markerLng:this.currentPlace.geometry.location.lng(),
                iconOptions: {
                    url:'../img/apteka.png',
                    size: {width: 60, height: 60, f: 'px', b: 'px',},
                    scaledSize: {width: 70, height: 70, f: 'px', b: 'px',},
                }
            });
            // console.log(this.markers)
            this.markerSearch = null
        },
        markerClick(params){
            window.open(params.url, '_blank')
        },
        setStyleMarker(e){
            console.log(e.title)
        }
    }
}
</script>

<style scoped>

</style>