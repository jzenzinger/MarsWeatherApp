<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Weather</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true" class="ion-margin">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Astronomy Picture Of Day</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid class="ion-padding">
        <ion-row class="ion-align-items-center">
          <ion-col>
            <ion-button color="dark" @click="fetchApodData">Get APOD</ion-button>
          </ion-col>
        </ion-row>
        <ion-row class="ion-text-center">
          <ion-title>{{ apodArr.title }}</ion-title>
        </ion-row>
        <ion-row>
          <ion-col>
            {{ apodArr.date }}
          </ion-col>
          <ion-col>
            {{ apodArr.explanation }}
          </ion-col>
        </ion-row>
        <ion-row class="ion-padding">
          <ion-img :src="apodArr.url"></ion-img>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol } from '@ionic/vue';
import {defineComponent} from "vue";

export default defineComponent({
  name: 'Tab2',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonGrid, IonRow, IonCol },
  data() {
    return {
      apodArr: []
    }
  },
  methods: {
    async fetchApodData() {
      const url = 'https://api.nasa.gov/planetary/apod?api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2';
      fetch(url)
          .then(res => res.json())
          .then(data => this.apodArr = data)
          .catch(err => console.log(err.message))
    }
  }
})
</script>