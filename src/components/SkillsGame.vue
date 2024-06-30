<template>
    <ion-content>
        <ion-grid>
            <ion-row>
                <div v-for="skill in skills" :key="skill.id">
                    <ion-col>
                        <ion-card>
                            <ion-card-header>
                                <ion-card-title>{{ skill.name }}</ion-card-title>
                            </ion-card-header>
                            <ion-card-content>
                                <ion-chip>
                                    <ion-label>{{ skill.level }}</ion-label>
                                </ion-chip>
                            </ion-card-content>
                        </ion-card>
                    </ion-col>
                </div>
            </ion-row>
        </ion-grid>
    </ion-content>
</template>

<script lang="ts">
import axios from 'axios';
import { defineComponent, ref } from 'vue';
import {
    IonButton,
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardTitle,
    IonChip,
    IonCol,
    IonContent,
    IonGrid,
    IonLabel,
    IonRow,
} from '@ionic/vue';

interface Skill {
    id: number;
    name: string;
    level: string;
}

export default defineComponent({
    components: {
        IonButton,
        IonCard,
        IonCardContent,
        IonCardHeader,
        IonCardTitle,
        IonChip,
        IonCol,
        IonContent,
        IonGrid,
        IonLabel,
        IonRow,
    },
    setup() {
        const skills = ref<Skill[]>([]);
        axios
            .get('http://portfolio.test/api/skills')
            .then((response) => {
                skills.value = response.data;
                console.log(response.data);
            })
            .catch((error) => {
                console.error('There was an error fetching the informations:', error);
            });

        return {
            skills,
        };
    },
});
</script>

<style scoped>
ion-card {
    margin: 20px;
}

ion-chip {
    margin-top: 10px;
}
</style>