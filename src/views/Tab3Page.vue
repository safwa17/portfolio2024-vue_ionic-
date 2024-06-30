<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Contact</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
        </ion-toolbar>
      </ion-header>
      <ion-list>
        <ion-item>
          <ion-select label="Topic">
            <ion-select-option value="job offer">Job Offer</ion-select-option>
            <ion-select-option value="questions">Questions</ion-select-option>
            <ion-select-option value="collaboration">Collaboration</ion-select-option>
          </ion-select>
        </ion-item>
        <ion-item>
          <ion-input label="Text input" placeholder="Enter text"></ion-input>
        </ion-item>

        <ion-item>
          <ion-input label="Email input" type="email" placeholder="email@domain.com"></ion-input>
        </ion-item>
      </ion-list>
      <ion-button>Send</ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonInput, IonItem, IonList, IonSelect, IonSelectOption} from '@ionic/vue';
import { IonButton } from '@ionic/vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
</script>
