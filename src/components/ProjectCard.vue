<template>
  <div v-for="project in projects" :key="project.id">
    <ion-col>
      <ion-card>
        <ion-card-header>
          <ion-card-title>{{ project.title }}</ion-card-title>
          <ion-card-subtitle>{{ project.type }}</ion-card-subtitle>
        </ion-card-header>

        <ion-card-content>
          <p>{{ project.description }}</p>
          <ion-chip v-for="technology in project.technologies" :key="technology.id"
            :style="{ backgroundColor: technology.color }">
            <ion-icon aria-hidden="true" :icon="technology.icon" />
            <ion-label>{{ technology.name }}</ion-label>
          </ion-chip>
        </ion-card-content>
        <ion-button v-if="project.github_link" fill="clear" :href="project.github_link"
          target="_blank">GitHub</ion-button>
        <ion-button v-if="project.demo_link" fill="clear" :href="project.demo_link" target="_blank">Demo</ion-button>
      </ion-card>
    </ion-col>

  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IonButton, IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCol, IonIcon, IonLabel } from '@ionic/vue';
import axios from 'axios';
import { IonChip } from '@ionic/vue';
import { images, square, triangle, heart, albums, clipboard, accessibility, pin, logoJavascript } from 'ionicons/icons';

interface Technology {
  id: number;
  name: string;
  color: string;
  icon: string;
}

interface Project {
  id: number;
  title: string;
  type: string;
  description: string;
  image: string | null;
  github_link: string | null;
  demo_link: string | null;
  technologies: Technology[];
}

interface chipBG {
  color: string;
  icon: string;
}

const projects = ref<Project[]>([]);

const chipBG: { [key: number]: chipBG } = {
  1: { color: '#590D22', icon: 'logo-vscode' },
  2: { color: '#800F2F', icon: 'logo-ionic' },
  3: { color: '#A4133C', icon: 'logo-bootstrap' },
  4: { color: '#C9184A', icon: 'logo-wordpress' },
  5: { color: '#FF4D6D', icon: 'logo-laravel' },
  6: { color: '#FF758F', icon: 'logo-flask' },
  7: { color: '#FF8FA3', icon: 'logo-javascript' },
  8: { color: '#FFB3C1', icon: 'logo-react' },
  9: { color: '#FFCCD5', icon: 'logo-react-native' },
  10: { color: '#FFF0F3', icon: 'logo-figma' },
  11: { color: '#470A1C', icon: 'logo-android' },
};


axios.get('http://portfolio.test/api/projects')
  .then(response => {
    projects.value = response.data.map((project: Project) => {
      return {
        ...project,
        technologies: project.technologies.map(tech => ({
          ...tech,
          color: chipBG[tech.id]?.color || 'defaultColor',
          icon: chipBG[tech.id]?.icon || 'defaultIcon'
        }))
      };
    });
  })
  .catch(error => {
    console.error('There was an error fetching the projects:', error);
  });

</script>

<style scoped>
.project {
  margin-bottom: 20px;
}

ion-card {
  margin: 30px;
}

ion-chip {
  background: #ffb703;
  color: black;
}
</style>
