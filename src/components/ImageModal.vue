<template>
  <ion-modal [isOpen]="{{ isModalOpen }}" :swipe-to-close="true">
    <ng-template>
      <app-modal-content>
        <ion-img :src="imgSrc"></ion-img>
      </app-modal-content>
    </ng-template>
  </ion-modal>
</template>

<script lang="ts">

export default {
  name: "ImageModal",
  props: ['isModalOpen', 'imgSrc']
}
</script>

<style scoped>

</style>