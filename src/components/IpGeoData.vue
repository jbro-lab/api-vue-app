<template>
  <div class="hello">
    <h3>{{msg}}</h3>
    <p v-if="ipGeo">
     <span v-if="ipGeo.city">{{ipGeo.city}}, </span>
     <span v-if="ipGeo.regionName">{{ipGeo.regionName + ' '}} </span>
     <span v-if="ipGeo.zip">{{ipGeo.zip + ' '}} </span>
     <span v-if="ipGeo.country">{{ipGeo.country + ' '}} </span>
     <br>
     <span v-if="ipGeo.isp">ISP: {{ipGeo.isp + ' '}}<br></span>
     <span v-if="ipGeo.mobile != null">Is Mobile: {{ipGeo.mobile}}<br></span>
     <span v-if="ipGeo.ip">ip: {{ipGeo.ip}}</span>
     <span></span>
    </p>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';

export default defineComponent({
  name: 'IpGeoData',
  props: {
    msg: String,
  },
  setup() {
    const ip = ref('');
    const ipGeo = ref();
    onMounted(async () => {
      ip.value = await fetch('https://api.ipify.org?format=json')
        .then((response) => response.json())
        .then((response) => response.ip);
      ipGeo.value = await fetch(`https://api.techniknews.net/ipgeo/${ip.value}`)
        .then((response) => response.json())
        .then((response) => response);
    });
    return { ipGeo };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
