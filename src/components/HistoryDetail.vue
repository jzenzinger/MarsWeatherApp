<template>
  <ion-header>
    <ion-toolbar>
      <ion-title>{{ array.date }}</ion-title>
      <ion-subtitle class="smallText">Swipe down to close</ion-subtitle>
    </ion-toolbar>
  </ion-header>
  <ion-content class="ion-padding">
    <ion-label class="ion-text-center ion-padding-top">Copyright: {{ array.copyright }}</ion-label>
    <ion-img :src="array.url" class="ion-margin-vertical"></ion-img>
    <ion-label class="ion-padding">{{ array.explanation }}</ion-label>
  </ion-content>
</template>

<script lang="ts">

import { defineComponent } from "vue";
import { IonHeader, IonTitle, IonToolbar, IonContent, IonImg, IonLabel } from "@ionic/vue";

export default defineComponent({
  name: "ImageModal",
  props: ['array'],
  components: { IonHeader, IonTitle, IonToolbar, IonContent, IonImg, IonLabel },
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