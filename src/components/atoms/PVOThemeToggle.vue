<template>
    <div class="flex">
        <div class="mode-toggle" @click="modeToggle" :class="{ 'dark-mode-toggled': darkMode }">
            <div class="toggle">
                <div id="dark-mode" :class="{ rotate: isRotating }">
                    <v-icon>{{ darkMode ? 'mdi-weather-night' : 'mdi-white-balance-sunny' }}</v-icon>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useTheme } from 'vuetify'

const darkMode = ref(false)
const isRotating = ref(false)
const theme = useTheme()
const currentTheme = ref(theme.global.name.value)

function dark() {
    document.body.classList.add('dark-mode')
    darkMode.value = true
    theme.global.name.value = 'dark'
    currentTheme.value = 'dark'
}

function light() {
    document.body.classList.remove('dark-mode')
    darkMode.value = false
    theme.global.name.value = 'light'
    currentTheme.value = 'light'
}

function modeToggle() {
    isRotating.value = true
    setTimeout(() => {
        if (darkMode.value || document.body.classList.contains('dark-mode')) {
            light()
        } else {
            dark()
        }
        isRotating.value = false
    }, 500)
}

onMounted(() => {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
        dark()
    }
})
</script>

<style scoped>
$dark: #171717;
$mode-toggle-bg: #262626;

body {
    background-color: #fff;
    color: $dark;
    transition: background-color 0.2s ease, color 0.2s ease;
}

body.dark-mode {
    background-color: lighten($dark, 5%);

    .flex h1 {
        color: #fff;
    }
}

.mode-toggle {
    position: relative;
    padding: 0;
    width: 44px;
    height: 24px;
    background-color: $mode-toggle-bg;
    border: 1px solid #a5abba;
    border-radius: 24px;
    cursor: pointer;
    transition: background-color 0.5s ease, border-color 0.5s ease; 
    .toggle {
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        margin: auto;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 3px solid transparent;
        box-shadow: inset 0 0 0 2px #a5abba;
        overflow: hidden;
        transition: transform 0.5s ease;

        #dark-mode {
            position: relative;
            width: 100%;
            height: 100%;
            overflow: hidden;
            border-radius: 50%;

            &:before {
                content: '';
                position: relative;
                width: 100%;
                height: 100%;
                left: 50%;
                float: left;
                background-color: #a5abba;
                transition: border-radius 0.5s ease, width 0.5s ease, height 0.5s ease, left 0.5s ease, transform 0.5s ease;
            }
        }
    }
}

body.dark-mode .mode-toggle {
    background-color: lighten($mode-toggle-bg, 5%);
    border-color: #a5abba;

    .toggle {
        transform: translateX(19px);

        #dark-mode:before {
            border-radius: 50%;
            width: 150%;
            height: 85%;
            left: 40%;
            transform: translate(-10%, -40%) rotate(-35deg);
        }
    }
}

.v-icon {
    color: var(--v-theme-primary);
    transition: transform 0.5s ease-in-out, color 0.5s ease-in-out;
}

.rotate {
    transform: rotate(360deg);
}

html {
    font-size: 16px;
}

html, body, #app {
    width: 100%;
    height: 100%;
}

body {
    margin: 0;
    font-family: "Source Sans Pro", sans-serif;
}

h1 {
    font-weight: 400;
    transition: color 0.5s ease;
}
</style>
