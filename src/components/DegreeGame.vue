<template>
    <ion-list>
        <ion-reorder-group :disabled="false" @ionItemReorder="handleReorder($event)">
            <div v-for="educationItem in educations" :key="educationItem.id">
                <ion-item>
                    <ion-label> {{ educationItem.degree }} in {{ educationItem.institution }}</ion-label>
                    <ion-reorder slot="end"></ion-reorder>
                </ion-item>
            </div>
        </ion-reorder-group>
    </ion-list>

    <!-- <ion-button >Click Me</ion-button> -->
    <!-- <ion-alert :is-open="isOpen" header="A Short Title Is Best" sub-header="A Sub Header Is Optional"
        message="A message should be a short, complete sentence." :buttons="alertButtons"
        @didDismiss="setOpen(false)"></ion-alert> -->

</template>


<script lang="ts">
import axios from 'axios';
import { defineComponent, ref } from 'vue';
import { IonModal, IonHeader, IonContent, IonToolbar, IonTitle, IonPage, IonItem, IonLabel, IonList, IonReorder, IonReorderGroup } from '@ionic/vue';
import { IonAlert, IonButton, alertController } from '@ionic/vue';

// const isOpen = ref(false);
// const alertButtons = ['Action'];

// const setOpen = (state: boolean) => {
//     isOpen.value = state;
// };

const presentAlert = async () => {
    const alert = await alertController.create({
        header: 'Congrats ! ',
        subHeader: 'You know me a little better now',
        message: 'Dont stop here keep going !',
        buttons: ['Keep Going'],
    });

    await alert.present();
};


interface Education {
    id: number;
    degree: string;
    institution: string;
    start_date: string;
    end_date: string;
    description: string | null;
}

export default defineComponent({
    components: {
        IonButton, IonModal, IonHeader, IonContent, IonToolbar, IonTitle, IonPage, IonItem, IonLabel, IonList, IonReorder, IonReorderGroup
    },
    setup() {
        const page = ref<InstanceType<typeof IonPage> | null>(null);
        const modal = ref<InstanceType<typeof IonModal> | null>(null);
        const educations = ref<Education[]>([]);
        const items = ref([1, 2]);

        const expectedOrder = [1, 2];


        axios.get('http://portfolio.test/api/education')
            .then(response => {
                educations.value = response.data;
            })
            .catch(error => {
                console.error('There was an error fetching the informations:', error);
            });


        const handleReorder = (event: CustomEvent) => {
            console.log('Before complete', items.value);
            items.value = event.detail.complete(items.value);
            console.log('After complete', items.value);
            const isCorrectOrder = JSON.stringify(items.value) === JSON.stringify(expectedOrder);
            if (isCorrectOrder) {
                presentAlert()
            } else {
            }
        };


        return {
            page,
            modal,
            educations,
            handleReorder
        };
    }
});
</script>
