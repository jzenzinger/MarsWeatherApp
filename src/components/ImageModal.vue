<template>
  <ion-header>
    <ion-toolbar>
      <ion-title>Picture from {{ arrayPic.rover.name }}</ion-title>
      <ion-subtitle class="smallText">Swipe down to close</ion-subtitle>
    </ion-toolbar>
  </ion-header>
  <ion-content class="ion-padding">
    <ion-img :src="imgSrcModal"></ion-img>
    <ion-grid class="ion-margin ion-padding-top">
      <ion-row class="ion-align-items-center">
        <ion-col size="1">
          <ion-icon :icon="camera"></ion-icon>
        </ion-col>
        <ion-col size="11" class="ion-padding-start">
          <ion-card-subtitle>{{ arrayPic.camera.name }} - {{ arrayPic.camera.full_name }}</ion-card-subtitle>
        </ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="1">
          <ion-icon :icon="planet"></ion-icon>
        </ion-col>
        <ion-col class="ion-padding-start">
          <ion-card-subtitle> Sol {{ arrayPic.sol }}</ion-card-subtitle>
        </ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="1">
          <ion-icon :icon="rocket"></ion-icon>
        </ion-col>
        <ion-col class="ion-padding-start">
          <ion-card-subtitle> {{ arrayPic.rover.launch_date }}</ion-card-subtitle>
        </ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="1">
          <ion-icon :icon="calendar"></ion-icon>
        </ion-col>
        <ion-col class="ion-padding-start">
          <ion-card-subtitle> {{ arrayPic.rover.landing_date }}</ion-card-subtitle>
        </ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="1">
          <ion-icon :icon="build"></ion-icon>
        </ion-col>
        <ion-col class="ion-padding-start">
          <ion-card-subtitle> {{ arrayPic.rover.status }}</ion-card-subtitle>
        </ion-col>
      </ion-row>
    </ion-grid>
  </ion-content>
</template>

<script lang="ts">

import { defineComponent } from "vue";
import { IonHeader, IonTitle, IonToolbar, IonContent, IonCardSubtitle, IonGrid, IonRow, IonCol } from "@ionic/vue";
import { camera, car, calendar, rocket, build, planet } from "ionicons/icons";

export default defineComponent({
  name: "ImageModal",
  props: ['imgSrcModal', 'arrayPic'],
  components: { IonHeader, IonTitle, IonToolbar, IonContent, IonCardSubtitle, IonGrid, IonRow, IonCol },
  setup() {
    return {
      camera,
      car,
      calendar,
      rocket,
      build,
      planet
    }
  }
});
</script>

<style>
.smallText {
  color: rgba(255, 255, 255, 0.54);
  display: flex;
  margin: auto;
  padding-top: 30px;
  justify-content: center;
  font-size: 10px !important;
}
</style>