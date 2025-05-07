<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      
      <ion-input label="Badge count" type="number" :clear-input="true" 
        v-model="badgeCount"></ion-input>

      <ion-button expand="full" color="primary" @click="setBadgeCount">
        Set Badge Count</ion-button>
      <ion-button expand="full" color="primary" @click="clearBadgeCount">
        Mark as Read</ion-button>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonButton, IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonInput } from '@ionic/vue';
import { ref } from 'vue';

const badgeCount = ref(3);

const clearBadgeCount = async () => {
  badgeCount.value = 0;
  await setBadgeCount();
};

const setBadgeCount = async () => {
  if (badgeCount.value === 0) {
    navigator.clearAppBadge && await navigator.clearAppBadge();
  } else {
    navigator.setAppBadge && await navigator.setAppBadge(badgeCount.value)
  }
  const event = new CustomEvent("badgeCount", { detail: {badgeCount: badgeCount.value} });
  window.dispatchEvent(event);
};

</script>
