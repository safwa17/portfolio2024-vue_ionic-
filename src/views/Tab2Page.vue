<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My projects</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-grid>
        <ion-row>
          <project-card></project-card>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import ProjectCard from '@/components/ProjectCard.vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCol, IonGrid, IonRow } from '@ionic/vue';
</script>
