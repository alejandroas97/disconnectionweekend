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
const checked = ref(false);
const toast = useToast();

const logoUrl = computed(() => {
    return `layout/images/${layoutConfig.darkTheme.value ? 'logo-white' : 'logo-dark'}.svg`;
});



async function login(){
    if (email.value == "0" && password == '0') {
        try {
            const token="login-okay"
            localStorage.setItem('token', token);
            await router.push('/landing'); // Ajusta la ruta según tus necesidades
      } catch (error) {
        console.error('Error durante el inicio de sesión:', error);
      }
    } else {
        console.log('error en login')
        toast.add({ severity: 'error', summary: 'Login incorrecto', detail: 'Inténtalo de nuevo', life: 3000 });
    }
}



</script>

<template>
    <div class="surface-ground flex align-items-center justify-content-center min-h-screen min-w-screen overflow-hidden">
        <div class="flex flex-column align-items-center justify-content-center">
            <img :src="logoUrl" alt="Sakai logo" class="mb-5 w-6rem flex-shrink-0" />
            <div style="border-radius: 56px; padding: 0.3rem; background: linear-gradient(180deg, var(--primary-color) 10%, rgba(33, 150, 243, 0) 30%)">
                <Toast />
                <div class="w-full surface-card py-8 px-5 sm:px-8" style="border-radius: 53px">
                    <div class="text-center mb-5">
                        <img src="/demo/images/login/cindi.jpg" alt="Image" height="150" class="mb-5 img-fluid rounded-circle" style="transform: rotate(90deg); border-radius: 100%;"/>
                        <div class="text-900 text-3xl font-medium mb-3">Holaaaa, Cindiiii!</div>
                    </div>

                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        MUCHAS FELICIDADES <br>

                        Si has llegado hasta aquí es porque has seguido seguir viva un año más, enhorabuena. <br>
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Tu regalo de cumpleaños va a tener que esperar un poco todavía.
                        <ProgressBar :value="14"></ProgressBar>
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Han sido unos meses bastante complicados. Obras interminables, entre quitar y poner azulejos con mínimos
                        desperfectos, puertas que parecían no ponerse rectas nunca, y pinturas que no querían pegarse al techo.
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Ya toca parar, salir de casa y desconectar unos días.
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Pero, ¿a dónde?¿Qué vamos a hacer?
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Buena pregunta.
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Para saber más, vas a tener que ir pasando una serie de retos con los que,
                        día a día, irás descubriendo de qué se trata.
                    </div>
                    <div class="mx-auto text-wrap text-center mb-4 textAc">
                        Empecemos desvelando la fecha. Para ello necesitarás resolver estos sencillos (a priori)
                        acertijos.
                    </div>


                    <div>
                        <label for="email1" class="block text-900 text-xl font-medium mb-2">
                            <div class="mx-auto text-wrap text-center mb-4 textAc">
                                ¿Cuántos animales llevó Moisés en el arca?
                            </div>
                        </label>
                        <InputNumber v-model="value1" inputId="integeronly" />
                        <InputText id="email1" type="text" placeholder="Introduce un número" class="w-full md:w-30rem mb-5" style="padding: 1rem" v-model="email" />

                        <label for="password1" class="block text-900 font-medium text-xl mb-2">Contraseña</label>
                        <Password id="password1" v-model="password" placeholder="Password" :toggleMask="true" class="w-full mb-3" inputClass="w-full" :inputStyle="{ padding: '1rem' }"></Password>

                        <div class="flex align-items-center justify-content-between mb-5 gap-5">
                            <div class="flex align-items-center">
                                <Checkbox v-model="checked" id="rememberme1" binary class="mr-2"></Checkbox>
                                <label for="rememberme1">Remember me</label>
                            </div>
                            <a class="font-medium no-underline ml-2 text-right cursor-pointer" style="color: var(--primary-color)">Forgot password?</a>
                        </div>
                        <Button label="Sign In" class="w-full p-3 text-xl" @click="login()"></Button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <AppConfig simple />
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
