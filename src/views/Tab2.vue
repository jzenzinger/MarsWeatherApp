<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Weather</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Weather</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid class="ion-padding-lg">
        <ion-row class="ion-align-items-center">
          <ion-col>
            <ion-button color="dark" v-on:click="fetchWeatherData">Get Weather</ion-button>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col v-for="arr in weatherArr" :key = arr.id>
            {{ arr }}
          </ion-col>
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
      weatherArr: []
    }
  },
  methods: {
    async fetchWeatherData() {
      const url = 'https://api.nasa.gov/insight_weather/?api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2&feedtype=json&ver=1.0';
      fetch(url)
          .then(res => res.json())
          .then(data => this.weatherArr = data)
          .catch(err => console.log(err.message))
    }
  }
})
</script>