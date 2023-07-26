<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <ip-geo-data msg="Discover Your IP and Geolocation Data"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import IpGeoData from '@/components/IpGeoData.vue'; // @ is an alias to /src

export default defineComponent({
  name: 'HomeView',
  components: {
    IpGeoData,
  },
});
</script>
