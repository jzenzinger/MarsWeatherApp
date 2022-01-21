<template>
  <ion-page>
    <ion-content :scroll-event="true" class="ion-padding-top" ref="myContent">
      <!-- fab placed to the bottom end -->
      <ion-fab vertical="bottom" horizontal="end" slot="fixed" @click="handleFabClick">
        <ion-fab-button @click="handleFabClick">
          <ion-icon :icon="arrowUpCircle"></ion-icon>
        </ion-fab-button>
      </ion-fab>
      <ion-item class="ion-margin" lines="none">
        <ion-label>Camera</ion-label>
        <ion-select v-model="selectedCam" placeholder="Select one" interface="popover" @click="toggleLoaded">
          <ion-select-option v-for="cam in cameraArr"
                             :key="cam.name"
                             :value="cam.name">
            {{ cam.name }}
          </ion-select-option>
        </ion-select>
      </ion-item>
      <ion-content v-if="loaded === false" class="ion-padding">
        <ion-label class="ion-text-center"> Select which camera you want to see.</ion-label>
      </ion-content>
      <ion-grid v-if="loaded">
        <ion-row class="ion-align-items-center" v-for="pic in photosArr" :key="pic.id">
          <!-- Components template to render pictures in-->
          <ion-col size="12" v-if="selectedCam === pic.camera.name">
            <!-- Loading only cards from photosArr by selected camera -->
            <!-- Last 2 roversCard ChemCam and NavCam is showing on the down of page and don't know why -->
            <RoverCard :cam-full-name="pic.camera.full_name"
                       :camera-subtitle="pic.camera.name"
                       :rover-subtitle="pic.rover.name"
                       :img-src="pic.img_src"
                       :start-date="pic.rover.launch_date">
            </RoverCard>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">

import { IonPage, IonContent, IonGrid, IonCol, IonRow, IonItem, IonLabel, IonSelect, IonSelectOption, IonFab, IonFabButton } from '@ionic/vue';
import { defineComponent } from 'vue';
import { arrowUpCircle } from 'ionicons/icons';
import RoverCard from "@/components/RoverCard.vue";

export default defineComponent({
  name: 'Tab1',
  components: { RoverCard, IonContent, IonPage, IonGrid, IonCol, IonRow,  IonItem, IonLabel, IonSelect, IonSelectOption, IonFab, IonFabButton },
  data() {
    return {
      photosArr: [],
      cameraArr: [{ name: 'FHAZ'}, { name: 'RHAZ'}, { name:'MAST'}, { name:'NAVCAM'}, { name:'CHEMCAM'}],
      selectedCam: String,
      loaded: false,
    };
  },
  methods: {
    fetchRovers() {
      const url = "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2";
      fetch(url)
          .then(res => res.json())
          .then(data => this.photosArr = data.photos)
          .catch(err => console.log(err.message))
    },
    toggleLoaded() {
      this.loaded = true;
    },
    handleFabClick() {
      (this.$refs.myContent as any).scrollToTop();
    }
  },
  mounted() {
    this.fetchRovers();
  },
  setup() {
    return {
      arrowUpCircle,
    }
  },
});
</script>

<style scoped>
.ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
}
ion-item {
  --ion-item-background: transparent;
  --ion-text-color: rgb(255, 255, 255);
}
ion-select ion-select-option {
  --ion-text-color: rgb(255, 255, 255);
}
</style>