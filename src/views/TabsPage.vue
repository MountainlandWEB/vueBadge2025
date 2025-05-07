<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <ion-badge v-if="badgeCount > 0" color="danger">{{ badgeCount }}</ion-badge>
          <ion-icon aria-hidden="true" :icon="triangle" />
          <ion-label>Tab 1</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon aria-hidden="true" :icon="ellipse" />
          <ion-label>Tab 2</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon aria-hidden="true" :icon="square" />
          <ion-label>Tab 3</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { IonBadge, IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { ellipse, square, triangle } from 'ionicons/icons';
import { onUnmounted, ref } from 'vue';

// consume the badge count from the child component

const badgeCount = ref(3);

const onBadgeCount = (e: any) => updateBadgeCount(e.detail.badgeCount)

window.addEventListener('badgeCount', onBadgeCount)

onUnmounted(() => {
  window.removeEventListener('badgeCount', onBadgeCount);
})

const updateBadgeCount = (count: number) => {
  badgeCount.value = count;
}
</script>
