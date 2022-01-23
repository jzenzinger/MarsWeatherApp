<template>
  <ion-page>
    <ion-content :fullscreen="true" class="ion-margin">
      <ion-grid class="ion-padding">
        <ion-row class="ion-text-center" v-if="loaded === false">
          <ion-col class="ion-text-start">
            <ion-button color="dark" @click="fetchApodData">Get APOD</ion-button>
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

export default defineComponent({
  name: 'Tab2',
  components: { IonTitle, IonContent, IonPage, IonGrid, IonRow, IonIcon },
  data() {
    return {
      apodArr: [],
      loaded: false,
    }
  },
  methods: {
    async fetchApodData() {
      const url = 'https://api.nasa.gov/planetary/apod?api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2';
      fetch(url)
          .then(res => res.json())
          .then(data => this.apodArr = data)
          .catch(err => console.log(err.message))
      this.loaded = true;
    }
  },
  setup() {
    return {
      calendar,
    }
  }
})
</script>

<style scoped>
.ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
  /*--ion-background-color: url(".././assets/bg-1.jpg");*/
}
</style>