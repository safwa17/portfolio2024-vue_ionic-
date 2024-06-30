<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Get to know me</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true" class="ion-padding">
      <ion-grid>
        <ion-row>
          <ion-col>
            <infos-card></infos-card>
          </ion-col>
          <!-- <ion-col>
            <degree-game></degree-game>
          </ion-col> -->
        </ion-row>
        <ion-row>
          <ion-col>
            <skills-game></skills-game>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">

import {
  IonContent,
  IonFab,
  IonFabButton,
  IonGrid,
  IonPage,
  IonHeader,
  IonIcon,
  IonImg,
  IonRow,
  IonTitle,
  IonToolbar,
  IonCol,
} from '@ionic/vue';
import InfosCard from '@/components/InfosCard.vue'
import DegreeGame from '@/components/DegreeGame.vue'
import SkillsGame from '@/components/SkillsGame.vue'
</script>
