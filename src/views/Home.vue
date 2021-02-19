<template>
  <div class="home">
     <l-map v-model="zoom" v-model:zoom="zoom" :center="[50.851197406224735, 4.353026448669574]">
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></l-tile-layer>
      <l-marker
        v-for="provider in providers"
        :key="provider.properties.straat"
        :lat-lng="[provider.geometry.coordinates[1], provider.geometry.coordinates[0]]"
      >
        <l-icon
          icon-url="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Filled_Syringe_icon.svg/128px-Filled_Syringe_icon.svg.png"
          :icon-size="[45, 45]"
        />
        <l-popup>
          <h1>{{provider.properties.straat}}</h1>
          <h3>{{provider.properties.huisnr}}</h3>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import {
  LMap, LIcon, LMarker, LTileLayer, LPopup,
} from '@vue-leaflet/vue-leaflet';
import { ref } from 'vue';
import places from '../places.js';


export default {
  name: 'Home',
  components: {
    LMap,
    LTileLayer,
    LIcon,
    LMarker,
    LPopup,
  },
  setup() {
    const zoom = ref(8);

    console.log(places);

    return {
      zoom,
      providers: places,
    };
  },
};
</script>

<style lang="scss">
.home {
  width: 100%;
  height: 100%;
}
</style>
