<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <!-- Components template to render pictures in-->
      <ion-card v-for="pic in photosArr" :key="pic.id" class="photos">
        <ion-card-header class="ion-padding-horizontal">
          <ion-card-title>{{ pic.camera.full_name }}</ion-card-title>
          <ion-card-subtitle>Camera {{ pic.camera.name }}</ion-card-subtitle>
          <ion-card-subtitle>Rover {{ pic.rover.name }}</ion-card-subtitle>
        </ion-card-header>
        <ion-card-content>
          <ion-img :src="pic.img_src"></ion-img>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">

import { IonPage, IonContent, IonImg } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Tab1',
  components: { IonContent, IonPage, IonImg },
  data() {
    return {
      photosArr: [],
    };
  },
  methods: {
    fetchRovers() {
        const url = "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2";
        fetch(url)
            .then(res => res.json())
            .then(data => this.photosArr = data.photos)
            .catch(err => console.log(err.message))
    },
  },
  mounted() {
    this.fetchRovers();
  },
});
</script>

<style scoped>
.ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
}
</style>