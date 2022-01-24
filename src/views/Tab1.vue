<template>
  <ion-page>
    <ion-content :scroll-event="true" class="ion-padding-top" ref="myContent">
      <!-- fab placed to the bottom end -->
      <ion-fab vertical="bottom" horizontal="end" slot="fixed" @click="handleFabClick">
        <ion-fab-button @click="handleFabClick" color="primary">
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
      <!-- Grid If camera isn't selected -->
      <ion-grid v-if="loaded === false" class="ion-padding">
        <ion-row class="ion-text-center">
          <ion-textarea> Select which camera you want to see.</ion-textarea>
        </ion-row>
      </ion-grid>
      <!-- Grid If camera is selected -->
      <ion-grid v-if="loaded">
        <ion-row class="ion-align-items-center" v-for="pic in photosArr" :key="pic.id">
          <ion-col class="ion-text-center" v-if="pic === null">
            <ion-label class="ion-color-danger">No data in storage, error!</ion-label>
          </ion-col>
          <!-- Components template to render pictures in-->
          <ion-col size="12" v-if="selectedCam === pic.camera.name">
            <!-- Selected specific camera name -->
            <RoverCard :cam-full-name="pic.camera.full_name"
                       :camera-subtitle="pic.camera.name"
                       :rover-subtitle="pic.rover.name"
                       :img-src="pic.img_src"
                       :start-date="pic.rover.launch_date"
                       :array="pic">
            </RoverCard>
          </ion-col>
          <!-- Selected All -->
          <ion-col size="12" v-if="selectedCam === 'All'">
            <!-- Loading only cards from photosArr by selected camera -->
            <RoverCard :cam-full-name="pic.camera.full_name"
                       :camera-subtitle="pic.camera.name"
                       :rover-subtitle="pic.rover.name"
                       :img-src="pic.img_src"
                       :start-date="pic.rover.launch_date"
                       :array="pic">
            </RoverCard>
          </ion-col>
        </ion-row>
        <!-- Selected None -->
        <ion-row class="ion-text-center" v-if="selectedCam === 'None'">
          <ion-textarea> Select which camera you want to see.</ion-textarea>
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
import { Storage } from "@capacitor/storage";
//import { SplashScreen } from "@capacitor/splash-screen";

export default defineComponent({
  name: 'Tab1',
  components: { RoverCard, IonContent, IonPage, IonGrid, IonCol, IonRow,  IonItem, IonLabel, IonSelect, IonSelectOption, IonFab, IonFabButton },
  data() {
    return {
      photosArr: [],
      cameraArr: [{ name: 'None'}, { name: 'All'}, { name: 'FHAZ'}, { name: 'RHAZ'}, { name:'MAST'}, { name:'NAVCAM'}, { name:'CHEMCAM'}],
      selectedCam: '',
      loaded: false,

    };
  },
  methods: {
    fetchRovers() {
      const url = "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=WpJlub0x6H6V2V5s4ryXm2j7LTES4HRhGrpAdPi2";
      fetch(url)
          .then(res => res.json())
          .then(data => {
            const array = JSON.stringify(data.photos);
            Storage.set({
              key: 'PHOTOS_FROM_API_KEY',
              value: array,
            });
          })
          .catch(err => console.log(err.message))
      //await SplashScreen.hide();
    },
    toggleLoaded() {
      this.loaded = true;
    },
    handleFabClick() {
      // Not working properly as error show scrollToTop function is not defined but in IDE,
      // but in IDE it is defined as ionic function
      (this.$refs.myContent as any).scrollToTop(200);
    },
    async parsePhotos() {
      const res = JSON.parse((await Storage.get({ key: 'PHOTOS_FROM_API_KEY'})).value || '{}');
      if(res !== null) {
        this.photosArr = res;
      }
    }
  },
  mounted() {
    this.fetchRovers();
    this.parsePhotos();
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
  /*--ion-background-color: url(".././assets/bg-1.jpg");*/
}
ion-item {
  --ion-item-background: transparent;
  --ion-text-color: rgb(255, 255, 255);
}
ion-select ion-select-option {
  --ion-text-color: rgb(255, 255, 255);
}
</style>