<template>
  <div class="login">
    <div class="d-flex justify-center align-center login-form">
      <v-card
        class="w-75 h-75 d-flex flex-column align-center pa-4"
      >
		<v-card-title class="w-100">
            <div class="d-flex align-center justify-space-between mb-1">
                <h2>Bienvenido</h2>
                <PVOThemeToggle />
            </div>
            <h3>Ingresa tus datos para continuar</h3>
		</v-card-title>
		<v-card-text class="w-100 mt-16">
            <v-form 
                @submit.prevent 
                class="w-100"
            >
                <PVOInput
                    v-model="username"
                    label="Usuario"
                    placeholder="Ingresa tu usuario"
                    size="small"
                />
                <PVOInput
                    class="mt-5"
                    v-model="password"
                    label="Contraseña"
                    placeholder="Ingresa tu contraseña"
                    size="small"
                    type="password"
                />
                <div class="d-flex mt-4 justify-end">
                    <a href="#">¿Olvidaste tu contraseña?</a>
                </div>
                <PVOButton 
                    class="w-100 mt-10" 
                    text="Ingresar" 
                    color="blue" 
                    size="large" 
                    type="submit"
                />
            </v-form>
            <div class="d-flex justify-center align-center mt-7">
                <h4 class="mt-10">No tienes cuenta? <a href="#">Regístrate</a></h4>
            </div>
		</v-card-text>
      </v-card>
    </div>
    <div
      class="login-image d-flex justify-center align-center pa-3">
      <img src="../assets/Group.png" alt="login-image" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import PVOInput from "@/components/organisms/PVOInput.vue";
import PVOThemeToggle from "@/components/atoms/PVOThemeToggle.vue";
import PVOButton from "@/components/atoms/PVOButton.vue";
import { ref } from "vue";

const username = ref("");
const password = ref("");

</script>

<style scoped>
.login {
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100vh;
  width: 100vw;
}

.login-image {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--image-background);
}


.login-form {
  background-color: var(--form-background);
}

.login-image img {
  max-width: 100%;
  max-height: 50%;
  object-fit: contain;
}
</style>
