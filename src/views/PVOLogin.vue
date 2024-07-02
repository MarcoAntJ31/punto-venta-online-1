<template>
    <div class="login">
        <div class="login-form d-flex justify-center align-center">
            <v-card class="w-50 h-75 d-flex flex-column justify-center align-center pa-10">
            <!-- <PVOThemeToggle /> -->
            <h2>Bienvenido</h2>
            <h3>Ingresa tus datos para continuar</h3>
            <v-form class="w-100">
                <PVOInput 
                    v-model="username" 
                    label="Usuario" 
                    placeholder="Ingresa tu usuario"
                    size="small"
                />
                <PVOInput 
                    v-model="password" 
                    label="Contraseña" 
                    placeholder="Ingresa tu contraseña"
                    size="small"
                    type="password"
                />
                <div class="d-flex mt-3 justify-end">
                    <a href="#">¿Olvidaste tu contraseña?</a>
                </div>
                <PVOButton 
                    class="w-100"
                    text="Ingresar" 
                    color="blue"
                    size="large"
                />
            </v-form>
            <h4>No tienes cuenta? <a href="#">Regístrate</a></h4>
            </v-card>
        </div>
        <div class="login-image d-flex justify-center align-center pa-3">
            <img src="../assets/Group.png" alt="login-image" />
        </div>
    </div>
</template>

<script lang="ts" setup>
import PVOInput from '@/components/organisms/PVOInput.vue'
import PVOThemeToggle from '@/components/atoms/PVOThemeToggle.vue'
import PVOButton from '@/components/atoms/PVOButton.vue'
import { ref } from 'vue'

const username = ref('')
const password = ref('')
</script>

<style scoped>
.login {
    display: grid;
    grid-template-columns: 1fr 1fr;
    height: 100vh;
    width: 100vw;
}

.login-form {
    background-color: #f5f5f5;
}

.login-image {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #F4D03F;
}

.login-image img {
  max-width: 100%;
  max-height: 50%;
  object-fit: contain;
}


</style>
