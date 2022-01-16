<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <!--<ion-item v-if="loaded">
        <ion-label>Select camera</ion-label>
        <ion-select v-for="cam in camerasArr" :key="cam.id" >
          <ion-select-option value="{{ cam.camera.name }}">{{ cam.camera.name }}</ion-select-option>
        </ion-select>
      </ion-item>-->
      <ion-grid>
        <ion-row>
          <!-- Components template to render pictures in-->
          <ion-col size="6" v-for="(pic, index) in photosArr" :key="pic.id">
            <!-- Loading only first 25 photos from photosArr -->
            <RoverCard v-if="index <= 50" class="photos"
                       :cam-full-name="pic.camera.full_name"
                       :camera-subtitle="pic.camera.name"
                       :rover-subtitle="pic.rover.name"
                       :img-src="pic.img_src"
                       :start-date="pic.rover.launch_date">
            </RoverCard>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">

import { IonPage, IonContent, IonGrid, IonCol, IonRow } from '@ionic/vue';
import { defineComponent } from 'vue';
import RoverCard from "@/components/RoverCard.vue";

export default defineComponent({
  name: 'Tab1',
  components: {RoverCard, IonContent, IonPage, IonGrid, IonCol, IonRow,  /*IonItem, IonLabel, IonSelect, IonSelectOption*/ },
  data() {
    return {
      photosArr: [],
      camerasArr: [],
      roversArr: [],
      loaded: false
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
    pushArray(arr1: any[], arr2: any[]) {
      arr1.push(arr2);
    },
    getUniqueValues(arr: any[]) {
      arr = arr.filter((v, i, a) => a.indexOf(v) === i);
    },
  },
  mounted() {
    this.fetchRovers();
    this.pushArray(this.camerasArr, this.photosArr);
  },
});
</script>

<style scoped>
ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
}
ion-card {
  margin: 15px;
}
</style>