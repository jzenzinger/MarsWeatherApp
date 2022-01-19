<template>
  <ion-header>
    <ion-toolbar>
      <ion-title> Rover picture</ion-title>
    </ion-toolbar>
  </ion-header>
  <ion-content class="ion-padding">
    <ion-img :src="imgSrcModal"></ion-img>
  </ion-content>
</template>

<script lang="ts">

import { defineComponent } from "vue";
import { IonHeader, IonTitle, IonToolbar, IonContent } from "@ionic/vue";

export default defineComponent({
  name: "ImageModal",
  props: ['imgSrcModal'],
  components: { IonHeader, IonTitle, IonToolbar, IonContent },
});
</script>