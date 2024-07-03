<template>
    <v-toolbar>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
  
      <v-toolbar-title>{{ title }}</v-toolbar-title>
  
      <v-spacer></v-spacer>
  
      <PVOButton
        v-for="(btn, index) in buttons"
        :key="index"
        :icon="btn.icon"
        @click="btn.action"
      />
    </v-toolbar>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  import PVOButton from '../atoms/PVOButton.vue';
  
  const props = defineProps({
    color: {
      type: String,
      default: 'primary',
    },
    title: {
      type: String,
      required: true,
    },
    buttons: {
      type: Array,
      required: true,
    },
  });
  </script>