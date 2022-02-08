<template>
  <ion-page>
    <ion-content :fullscreen="true" class="ion-margin">
      <ion-grid class="ion-padding ion-justify-content-center">
        <ion-row class="ion-padding-top">
          <ion-card-title class="ion-text-center ion-padding">Astronomy Picture Of Day</ion-card-title>
        </ion-row>
        <ion-row class="ion-margin-vertical" v-if="loaded === false">
          <ion-col class="ion-text-center">
            <ion-button color="dark" @click="parsePhotos">Get APOD</ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>
      <ion-grid class="ion-padding" v-if="loaded">
        <ion-row class="ion-text-start">
          <ion-col>
            <ion-title>{{ apodArr.title }}</ion-title>
          </ion-col>
        </ion-row>
        <ion-row class="ion-padding-top">
          <ion-img :src="apodArr.url"></ion-img>
        </ion-row>
        <ion-row class="ion-padding-top ion-padding-start">
          <ion-subtitle><ion-icon :icon="calendar" class="ion-padding-end"></ion-icon> {{ apodArr.date }}</ion-subtitle>
        </ion-row>
        <ion-row class="ion-padding">
            <ion-label>{{ apodArr.explanation }}</ion-label>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonTitle, IonContent, IonGrid, IonRow, IonIcon } from '@ionic/vue';
import {defineComponent} from "vue";
import { calendar } from "ionicons/icons";
import { Storage } from "@capacitor/storage";

export default defineComponent({
  name: 'Tab2',
  components: { IonTitle, IonContent, IonPage, IonGrid, IonRow, IonIcon },
  data() {
    return {
      apodArr: [],
      loaded: false,
      apodArrKey: 'APOD_FROM_API_KEY',
    }
  },
  methods: {
    async fetchApodData() {
      const url = 'https://api.nasa.gov/planetary/apod?api_key=INSERT_YOUR_API_KEY';
      fetch(url)
          .then(res => res.json())
          .then(async data => {
            //let array = [];
            //array = JSON.parse((await Storage.get({key: this.apodArrKey})).value || '{}');
            //if(array !== null || array.length !== 0) {
            //  array.concat(data);
            //}
            const stringArray = JSON.stringify(data);
            await Storage.set({
              key: this.apodArrKey,
              value: stringArray,
            });
          })
          .catch(err => console.log(err.message))
    },
    async parsePhotos() {
      const res = JSON.parse((await Storage.get({ key: this.apodArrKey})).value || '{}');
      if(res !== null) {
        this.loaded = true;
        this.apodArr = res;
      }
    },
  },
  setup() {
    return {
      calendar,
    }
  },
  mounted() {
    this.fetchApodData();
  }
})
</script>

<style scoped>
.ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
  /*--ion-background-color: url(".././assets/bg-1.jpg");*/
}
</style>
