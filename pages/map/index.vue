<template lang="pug">
.app
  .navbar
    .container 
      .row
        .col-3
          nuxt-link.main-button.p20(to="/") home

  #map
</template>
<style>
h1,
h2 {
  margin-top: 20px;
  padding: 13px 22px;
}
.inline {
  display: flex;
  align-items: baseline;
  justify-content: right;
  flex-direction: row;
}
#map {
  width: 100%;
  height: 100vh;
}
#map .mapboxgl-popup-content {
  font-family: europa, sans-serif;
  --text-opacity: 1;
  color: #fff;
  color: rgba(255, 255, 255, var(--text-opacity));
  --bg-opacity: 1;
  background-color: #6c63ff;
  background-color: #6c63ff;
  padding: 10px 10px 15px;
  border-radius: 10px;
  padding: 4rem 1.5rem 3rem;
}
.mapboxgl-popup-content {
  position: relative;
  background: #6c63ff;
  border-radius: 3px;
  box-shadow: 0 1px 2px #6c63ff;
  padding: 10px 10px 15px;
  pointer-events: auto;
}
#map .mapboxgl-popup-anchor-bottom .mapboxgl-popup-tip,
#map .mapboxgl-popup-anchor-bottom-left .mapboxgl-popup-tip,
#map .mapboxgl-popup-anchor-bottom-right .mapboxgl-popup-tip {
  border-top-color: #6c63ff;
}
.mapboxgl-popup-anchor-bottom .mapboxgl-popup-tip {
  -webkit-align-self: center;
  align-self: center;
  border-bottom: none;
  border-top-color: #fff;
}
.mapboxgl-popup-tip {
  border: 2rem solid transparent;
}
.mapboxgl-popup-tip {
  width: 0;
  height: 0;
  border: 10px solid transparent;
  z-index: 1;
}
*,
:after,
:before {
  box-sizing: border-box;
  border: 0 solid #e2e8f0;
}

.main-button {
  background-color: #55198b;
  border: solid 1px #55198b;
  color: white;
  font-weight: 700;
  width: max-content;
  padding: 13px 22px;
  margin-right: 50px;
  text-transform: uppercase;
  border-radius: 6px;
  text-align: center;
  text-decoration: none;
  display: block;

  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s ease-in-out 0s;
}
.main-button:hover {
  background-color: #ffffff;
  color: #55198b;
  transition: all 0.3s ease 0s;
}
</style>
<script>
import axios from "axios";
import mapboxgl from "mapbox-gl";
export default {
  head: {
    link: [
      {
        rel: "stylesheet",
        href: "https://api.mapbox.com/mapbox-gl-js/v1.10.0/mapbox-gl.css",
      },
    ],
  },
  data() {
    return {
      apiKey:
        "pk.eyJ1IjoiYW11cHhtIiwiYSI6ImNraHFiemYwbTA1emIycG10cDhnaHAwM3QifQ.CbdtwT7BEw0RDWcAF8bB4Q",
      center: [51.420296, 35.732379],
      sats: {},
      sats_count: 0,
    };
  },
  methods: {
    getCount: function () {
      if (process.client) {
        let data = this.$twemoji.parse(`  🚀 count ${this.sats_count}`);
        return data;
      }
    },
  },
  mounted() {
    if (process.client) {
      const mapboxgl = require("mapbox-gl");
      const map = new mapboxgl.Map({
        accessToken: this.apiKey,
        container: "map",
        style: "mapbox://styles/mapbox/streets-v9",
        center: [51.420296, 35.732379],
        zoom: 3,
      });
      axios
        .get("https://api.spacexdata.com/v4/starlink")
        .then(async (response) => {
          let data = response.data;
          this.sats_count = data.length;
          data.map((sat, index) => {
            if (
              90 > sat.latitude &&
              sat.latitude > -89 &&
              90 >= sat.longitude &&
              sat.longitude > -90
            ) {
              const LngLat = [sat.longitude * 1.75, sat.latitude * 1.5];

              let popup = `<h3 class="font-bold">star sat : ${index}</h3>`;
              popup += `<br><p><a href="/gallery/${sat.launch}">View launch details</a></p>`;
              const element = document.createElement("div");
              element.className = "marker";
              element.style.backgroundImage =
                "url('https://mokaramifar.ir/gps.svg')";
              element.style.width = "50px";
              element.style.height = "50px";
              element.addEventListener("click", (e) => {
                if (this.selectedMarker) {
                  this.selectedMarker.classList.remove("hidden");
                }

                this.selectedMarker = e.target;
                this.selectedMarker.classList.add("hidden");
                this.map.flyTo({ center: LngLat, speed: 0.5 });
              });
              const popupElement = new mapboxgl.Popup({
                offset: 0,
                anchor: "bottom",
              }).setHTML(popup);
              popupElement.on("close", () => {
                if (this.selectedMarker) {
                  this.selectedMarker.classList.remove("hidden");
                }
              });

              var el = document.createElement("div");
              el.id = "marker";
              new mapboxgl.Marker({ element, offset: [0, -20] })
                .setLngLat(LngLat)
                .setPopup(popupElement)
                .addTo(map);
            }
          });
        });
    }
  },
};
</script>