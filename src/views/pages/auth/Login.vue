<script setup>
import { useLayout } from '@/layout/composables/layout';
import { ref, computed } from 'vue';
import AppConfig from '@/layout/AppConfig.vue';
import router from '@/router';
import { useToast } from 'primevue/usetoast';
import ProgressBar from 'primevue/progressbar';
import InputNumber from 'primevue/inputnumber';

const { layoutConfig } = useLayout();
const email = ref('');
const password = ref('');
const password2 = ref('');
const checked = ref(false);
const toast = useToast();

const logoUrl = computed(() => {
    return `layout/images/${layoutConfig.darkTheme.value ? 'logo-white' : 'logo-dark'}.svg`;
});



async function login(){
    if (email.value == 45 && password.value == 28 && password2.value == 21104) {
        try {
            const token="login-okay"
            const ahora = new Date();
            localStorage.setItem('tiempoInicioSesion', ahora.getTime().toString()); 
            await router.push('/landing'); // Ajusta la ruta según tus necesidades
      } catch (error) {
        console.error('Error durante el inicio de sesión:', error);
      }
    } else {
        toast.add({ severity: 'error', summary: 'Respuesta incorrecta', detail: 'Inténtalo de nuevo', life: 3000 });
    }
}

const duracionMaximaSesion = 10 * 60 * 1000; // 30 minutos en milisegundos

setInterval(() => {
    console.log('mirando');
  const tiempoInicioSesion = localStorage.getItem('tiempoInicioSesion');

  if (tiempoInicioSesion) {
    const tiempoTranscurrido = new Date().getTime() - parseInt(tiempoInicioSesion, 10);

    if (tiempoTranscurrido > duracionMaximaSesion) {

      localStorage.removeItem('tiempoInicioSesion');

    }
  }
}, 60000); // Verificar cada minuto (ajusta según sea necesario)



</script>

<template>
    <div class="surface-ground flex align-items-center justify-content-center min-h-screen min-w-screen overflow-hidden">
        <div class="flex flex-column align-items-center justify-content-center">
            <div style="border-radius: 56px; padding: 0.3rem; background: linear-gradient(180deg, var(--primary-color) 10%, rgba(33, 150, 243, 0) 30%)">
                <Toast />
                <div class="w-full surface-card py-8 px-5 sm:px-8" style="border-radius: 53px">
                    <div class="text-center mb-5">
                        <img src="/demo/images/login/cindi.jpg" alt="Image" height="150" class="mb-5 img-fluid rounded-circle" style="transform: rotate(90deg); border-radius: 100%;"/>
                        <div class="text-900 text-3xl font-medium mb-3">Holaaaa, Cindiiii!</div>
                    </div>

                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Enhorabuena, has completado el primer reto <br>
                    </div>

                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        <ProgressBar :value="29"></ProgressBar>
                    </div>

                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Ahora tocará saber un poco más sobre la ubicación de las actividades que 
                        acontecerán en el fin de semana del 2 al 4 de febrero de 2024
                    </div>


                    <div>
                        <label for="email1" class="block text-900 text-xl font-medium mb-2">
                            <div class="mx-auto text-wrap text-center mb-4 textAc">
                                Si un triángulo tiene un ángulo de 90 grados y otro ángulo de 45 grados, ¿cuántos grados tiene el tercer ángulo?
                            </div>
                        </label>
                        <InputText id="email1" type="number" placeholder="Introduce un número" class="w-full md:w-30rem mb-5" style="padding: 1rem" v-model="email" />
                        
                        <label for="password" class="block text-900 text-xl font-medium mb-2">
                            <div class="mx-auto text-wrap text-center mb-4 textAc">
                                ¿Qué número corresponde para seguir la serie? <br> 1, 3, 6, 10, 15, 21 …
                            </div>
                        </label>
                        <InputText id="password" type="number" placeholder="Introduce un número" class="w-full md:w-30rem mb-5" style="padding: 1rem" v-model="password" />

                        <label for="password2" class="block text-900 text-xl font-medium mb-2">
                            <div class="mx-auto text-wrap text-center mb-4 textAc">
                                De acuerdo con las siguientes ecuaciones, tienes que adivinar cuál es la respuesta para la cuarta ecuación. 
                                <br> 8 + 2 = 16106
                                <br> 5 + 4 = 2091
                                <br> 9 + 6 = 54153
                                <br> 7 + 3 = ?
                            </div>
                        </label>
                        <InputText id="password2" type="number" placeholder="Introduce un número" class="w-full md:w-30rem mb-5" style="padding: 1rem" v-model="password2" />
                        <Button label="Listo" class="w-full p-3 text-xl" @click="login()"></Button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.pi-eye {
    transform: scale(1.6);
    margin-right: 1rem;
}

.pi-eye-slash {
    transform: scale(1.6);
    margin-right: 1rem;
}

.textAc {
    width: 20rem;
}
</style>
