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
            <ion-button color="dark" v-on:click="openAlert()">Dark</ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol } from '@ionic/vue';

export default  {
  name: 'Tab2',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonGrid, IonRow, IonCol },
  methods: {
    async openAlert() {
      const message = "Testing something...";
      alert(message);
    }
  }
}
</script>