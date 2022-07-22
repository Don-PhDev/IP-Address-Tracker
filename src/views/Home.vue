<template>
  <div class="flex flex-col h-screen max-h-screen">
    <div
      class="z-20 flex justify-center relative bg-hero-bg bg-cover px-4 pt-8 pb-32"
    >
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">
          IP Address Tracker
        </h1>
        <div class="flex">
          <input
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
            type="text"
            placeholder="Search for IP address or leave empty to get your IP info"
          >
          <i class="
            cursor-pointer
            bg-black text-white
            px-4 text-lg
            rounded-tr-md rounded-br-md
            flex items-center
            fas fa-chevron-right"
          ></i>
        </div>
      </div>
      <IPInfo />
    </div>
    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script>
import IPInfo from '../components/IPInfo.vue'
import leaflet from "leaflet"
import { onMounted } from 'vue'

export default {
  name: 'Home',
  components: {
    IPInfo
  },
  setup() {
    let map

    onMounted(() => {
      map = leaflet.map('map').setView([51.505, -0.09], 13)

      leaflet
        .tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
          maxZoom: 19,
          attribution: '© OpenStreetMap'
        }).addTo(map)
    })
  },
}
</script>
