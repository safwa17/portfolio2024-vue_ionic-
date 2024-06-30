<template>
    <IonText>Who am I?</IonText>
    <div id="button-container">
        <ion-button fill="outline" @click="showContent">Click here to discover</ion-button>
    </div>
    <div v-if="isShown" v-for="info in infos" :key="info.id">
        <ion-text>
            <h1>Hello, I'm <ion-text id="info">{{ info.name }}</ion-text></h1>
        </ion-text>
        <p>
            <ion-text>I'm a <ion-text id="info">{{ info.status }}</ion-text> and <ion-text id="info">{{ info.age
                    }}</ion-text>. Here is my email <ion-text id="info">{{ info.email }}</ion-text>, the link to my
                GitHub profile <a :href="info.github" target="_blank">{{ info.github }}</a>, and to my LinkedIn as well
                <a :href="info.linkedin" target="_blank">{{ info.linkedin }}</a>.
            </ion-text>
        </p>
    </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import { IonText, IonButton } from '@ionic/vue';
import axios from 'axios';

const isShown = ref(false);

function showContent() {
    isShown.value = !isShown.value;
}


// Fetching basic information from the API
interface Info {
    id: number;
    full_name: string;
    name: string;
    status: string;
    age: number;
    email: string;
    phone: string;
    github: string;
    linkedin: string;
}

const infos = ref<Info[]>([]);
axios.get('http://portfolio.test/api/infos')
    .then(response => {
        infos.value = response.data;
    })
    .catch(error => {
        console.error('There was an error fetching the information:', error);
    });
</script>


<style scoped>
.project {
    margin-bottom: 20px;
}

ion-card {
    margin: 40px;
}

ion-text {
    font-size: x-large;
    line-height: 70px;
}

#info {
    color: rgb(226, 43, 174);
}

#buttoncontainer {
    display: flex;
    text-align: center;
    justify-content: center;
    margin: 20 0px;
}
</style>