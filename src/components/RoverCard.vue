<template>
  <ion-card class="photos">
    <ion-card-header class="ion-padding-horizontal">
      <ion-card-title>{{ camFullName }}</ion-card-title>
      <ion-card-subtitle><ion-icon :icon="camera"></ion-icon> {{ cameraSubtitle }}</ion-card-subtitle>
      <ion-card-subtitle><ion-icon :icon="car"></ion-icon> {{ roverSubtitle }}</ion-card-subtitle>
      <ion-card-subtitle><ion-icon :icon="calendar"></ion-icon> {{ startDate }}</ion-card-subtitle>
    </ion-card-header>
    <ion-card-content>
      <ion-img :src="imgSrc" @click="setOpen(true)"></ion-img>
      <ion-modal :is-open="isModalOpen"
                 :swipe-to-close="true"
                 :breakpoints="[0.1, 0.5, 1]"
                 :initialBreakpoint="0.5"
                 @didDismiss="setOpen(false)">
        <ImageModal :img-src-modal="imgSrc"></ImageModal>
      </ion-modal>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts">

import { camera, car, calendar } from 'ionicons/icons';
import { defineComponent, ref } from "vue";
import ImageModal from "@/components/ImageModal.vue";
import { IonModal, IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle, IonIcon, IonImg, IonCardContent } from "@ionic/vue";

export default defineComponent( {
  name: "RoverCard",
  components: { ImageModal, IonModal, IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle, IonIcon, IonImg, IonCardContent },
  props: ['camFullName', 'cameraSubtitle', 'roverSubtitle', 'imgSrc', 'startDate'],
  setup() {
    const isModalOpen = ref(false);
    const setOpen = (state: boolean) => isModalOpen.value = state;
    return {
      isModalOpen,
      setOpen,
      camera,
      car,
      calendar
    }
  },
})
</script>