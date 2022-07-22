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
            v-model="queryIP"
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
            type="text"
            placeholder="Search for IP address or leave empty to get your IP info"
          >
          <i
            @click="getIpInfo"
            class="
              cursor-pointer
              bg-black text-white
              px-4 text-lg
              rounded-tr-md rounded-br-md
              flex items-center
              fas fa-chevron-right"
            >
          </i>
        </div>
      </div>
      <IPInfo v-if="ipInfo" :ipInfo="ipInfo" />
    </div>
    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script>
import IPInfo from '../components/IPInfo.vue'
import leaflet from "leaflet"
import { onMounted, ref } from 'vue'
import axios from "axios"

export default {
  name: 'Home',
  components: {
    IPInfo
  },
  setup() {
    let map
    const queryIP = ref("")
    const ipInfo = ref(null)

    onMounted(() => {
      map = leaflet.map('map').setView([14.5995, 120.9842], 10)

      leaflet
        .tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
          maxZoom: 19,
          attribution: '© OpenStreetMap'
        }).addTo(map)
    })

    const getIpInfo = async () => {
      try {
        const data = await axios.get(
          `https://geo.ipify.org/api/v2/country?apiKey=at_QpMy2anXNQtJ3BWixzcJi0gqWHB6j&ipAddress=${queryIP.value}`
        )
        const result = data.data
        ipInfo.value = {
          address: result.ip,
          state: result.location.region,
          timezone: result.location.timezone,
          isp: result.isp,
          lat: result.location.lat,
          lng: result.location.lng,
        }
        leaflet.marker([ipInfo.value.lat, ipInfo.value.lng]).addTo(map)
        map.setView([ipInfo.value.lat, ipInfo.value.lng], 13)
      } catch (error) {
        alert(error.message)
      }
    }

    return { queryIP, ipInfo, getIpInfo }
  },
}
</script>
