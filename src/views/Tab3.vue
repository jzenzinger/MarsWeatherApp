<template>
  <ion-page>
    <ion-content class="ion-padding-top">
      <ion-list v-if="loaded" class="ion-margin-top">
        <ion-label class="ion-text-center ion-color-danger" v-if="apodArr === null">
          No data in storage, error!
        </ion-label>
        <ion-item @click="setOpen(true)">
          <ion-label class="ion-text-start" :value="apodArr.title">{{ apodArr.title }}</ion-label>
          <ion-label class="ion-text-end" :value="apodArr.date">{{ apodArr.date }}</ion-label>

          <ion-modal :is-open="isModalOpen"
                     :swipe-to-close="true"
                     :initialBreakpoint="0.5"
                     @didDismiss="setOpen(false)" class="ion-margin-vertical">
            <history-detail :array="apodArr"></history-detail>
          </ion-modal>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonContent, IonList, IonItem, IonLabel, IonModal } from "@ionic/vue";
import { Storage } from "@capacitor/storage";
import { defineComponent, ref } from "vue";
import HistoryDetail from "@/components/HistoryDetail.vue";

export default defineComponent( {
  name: "Tab3",
  components: { IonPage, IonContent, IonList, IonItem, IonLabel, IonModal, HistoryDetail },
  data() {
    return {
      loaded: false,
      apodArrKey: 'APOD_FROM_API_KEY',
      apodArr: [],
    }
  },
  methods: {
    async parsePhotos() {
      const res = JSON.parse((await Storage.get({ key: this.apodArrKey})).value || '{}');
      if(res !== null) {
        this.toggleLoaded();
        this.apodArr = res;
      }
    },
    toggleLoaded() {
      this.loaded = true;
    },
  },
  mounted() {
    this.parsePhotos();
  },
  setup() {
    const isModalOpen = ref(false);
    const setOpen = (state: boolean) => isModalOpen.value = state;
    return {
      isModalOpen,
      setOpen,
    }
  },
})
</script>

<style scoped>
.ion-page {
  --ion-background-color: linear-gradient(0deg, rgba(54,10,2,1) 0%, rgba(143,47,32,1) 62%, rgba(207,55,10,1) 100%);
  /*--ion-background-color: url(".././assets/bg-1.jpg");*/
}
ion-item {
  --ion-item-background: #2f2f2f;
  --ion-text-color: rgb(255, 255, 255);
}
ion-select ion-select-option {
  --ion-text-color: rgb(255, 255, 255);
}
</style>