<template>
  <ion-card class="photos">
    <ion-card-header class="ion-padding-horizontal">
      <ion-card-title>{{ camFullName }}</ion-card-title>
      <ion-card-subtitle><ion-icon :icon="camera"></ion-icon> {{ cameraSubtitle }}</ion-card-subtitle>
      <ion-card-subtitle><ion-icon :icon="car"></ion-icon> {{ roverSubtitle }}</ion-card-subtitle>
      <ion-card-subtitle><ion-icon :icon="calendar"></ion-icon> {{ startDate }}</ion-card-subtitle>
    </ion-card-header>
    <ion-card-content>
      <ion-img :src="imgSrc" @click="toggleModalOpen"></ion-img>
    </ion-card-content>
  </ion-card>
  <div v-if="isModalOpen">
    <ion-modal :is-open="isModalOpen" :swipe-to-close="true" :fullscreen="true">
      <ng-template>
        <app-modal-content>
          <ion-img :src="imgSrc"></ion-img>
        </app-modal-content>
      </ng-template>
    </ion-modal>
  </div>
</template>

<script lang="ts">

import { camera, car, calendar } from 'ionicons/icons';
import {defineComponent} from "vue";

export default defineComponent( {
  name: "RoverCard",
  props: ['camFullName', 'cameraSubtitle', 'roverSubtitle', 'imgSrc', 'startDate'],
  data() {
    return {
      isModalOpen: false,
    };
  },
  methods: {
    toggleModalOpen() {
      this.isModalOpen = !this.isModalOpen;
    },
  },
  setup() {
    return {
      camera,
      car,
      calendar
    }
  },
})
</script>