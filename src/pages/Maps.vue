<template>
  <div id="map"></div>
</template>

<script>
import { API_KEY } from "./API_KEY";
import {Loader, LoaderOptions} from 'google-maps';

const loader = new Loader(API_KEY);
var iconBase = 'http://maps.google.com/mapfiles/kml/paddle/';
var icons = {
  danger: {
    icon: iconBase + 'pink-blank.png'
  },
  alert: {
    icon: iconBase + 'ylw-blank.png'
  },
  normal: {
    icon: iconBase + 'ltblu-blank.png'
  }
};

export default {
  created() {
    loader.load().then(function (google) {
      var myLatlng = new google.maps.LatLng(21.002984, 105.845009);
      var mapOptions = {
        zoom: 13,
        center: myLatlng,
        // scrollwheel: false, // we disable de scroll over the map, it is a really annoing when you scroll through page
        // styles: [
        //   {
        //     featureType: "water",
        //     stylers: [
        //       { saturation: 43 },
        //       { lightness: -11 },
        //       { hue: "#0088ff" }
        //     ]
        //   },
        //   {
        //     featureType: "road",
        //     elementType: "geometry.fill",
        //     stylers: [
        //       { hue: "#ff0000" },
        //       { saturation: -100 },
        //       { lightness: 99 }
        //     ]
        //   },
        //   {
        //     featureType: "road",
        //     elementType: "geometry.stroke",
        //     stylers: [{ color: "#808080" }, { lightness: 54 }]
        //   },
        //   {
        //     featureType: "landscape.man_made",
        //     elementType: "geometry.fill",
        //     stylers: [{ color: "#ece2d9" }]
        //   },
        //   {
        //     featureType: "poi.park",
        //     elementType: "geometry.fill",
        //     stylers: [{ color: "#ccdca1" }]
        //   },
        //   {
        //     featureType: "road",
        //     elementType: "labels.text.fill",
        //     stylers: [{ color: "#767676" }]
        //   },
        //   {
        //     featureType: "road",
        //     elementType: "labels.text.stroke",
        //     stylers: [{ color: "#ffffff" }]
        //   },
        //   { featureType: "poi", stylers: [{ visibility: "off" }] },
        //   {
        //     featureType: "landscape.natural",
        //     elementType: "geometry.fill",
        //     stylers: [{ visibility: "on" }, { color: "#b8cb93" }]
        //   },
        //   { featureType: "poi.park", stylers: [{ visibility: "on" }] },
        //   {
        //     featureType: "poi.sports_complex",
        //     stylers: [{ visibility: "on" }]
        //   },
        //   { featureType: "poi.medical", stylers: [{ visibility: "on" }] },
        //   {
        //     featureType: "poi.business",
        //     stylers: [{ visibility: "simplified" }]
        //   }
        // ]
      };
      this.$axios.get("http://localhost:5000/dashboard")
      .then(response => {
        // this.data_db = response.data;
        console.log(response);
      })
      .catch(e => {
        this.errors.push(e);
      });
      var map = new google.maps.Map(document.getElementById("map"), mapOptions);

      var center = new google.maps.Marker({
        position: myLatlng,
        title: "Hello World!"
      });
      
      var marker = new google.maps.Marker({
        position: new google.maps.LatLng(21.003424, 105.841060),
        title: "Hello World!"
      });
      

      // To add the marker to the map, call setMap();
      center.setMap(map);
      marker.setMap(map);
    });
  }
};
</script>
