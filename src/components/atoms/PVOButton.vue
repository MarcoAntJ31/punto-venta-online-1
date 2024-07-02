<template>
    <v-btn v-if="icon" icon>
      <v-icon>{{ icon }}</v-icon>
    </v-btn>
    <v-btn v-else
        :color="aButtonColor"
        :variant="variant" 
        :size="size"
        :loading="loading"
    >
      {{ text }}
    </v-btn>
  </template>

<script lang="ts">

export type AButtonColors = 'base' | 'blue' | 'purple' | 'green' | 'red' | 'yellow'
export type AButtonSizes = 'x-small' | 'small' | 'default' | 'large' | 'x-large'
export type AButtonVariants = 'text' | 'flat' | 'elevated' | 'tonal' | 'outlined' | 'plain' | 'radio'

</script>
  
  <script lang="ts" setup>
  import { defineProps, computed, PropType } from 'vue';
  
  const props = defineProps({
    color: {
        type: String as PropType<AButtonColors>,
        default: 'base'
    },
    variant: {
        type: String as PropType<AButtonVariants>,
        default: 'flat'
    },
    size: {
        type: String as PropType<AButtonSizes>,
        default: 'default'
    },
    icon: {
      type: String,
      required: false,
    },
    text: {
      type: String,
      required: false,
    },
    loading: {
        type: Boolean,
        default: false
    },
  });

  const aButtonColor = computed(() => {
    switch (props.color) {
        case 'base':
            if (props.variant === 'outlined' || props.variant === 'text') {
                return '#6B6C6D';
            }
            return '#F7F9FA';
        case 'blue':
            return '#85C1E9';
        case 'purple':
            return '#AF7AC5';
        case 'green':
            return '#65D740';
        case 'red':
            return '#FF4040';
        case 'yellow':
            if (props.variant === 'outlined' || props.variant === 'text') {
                return '#C37500';
            }
            return '#F4D03F';
        default:
            return '#F7F9FA'; 
    }
});
  </script>