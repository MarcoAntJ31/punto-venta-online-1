<template>
  <v-btn v-if="icon" icon>
    <v-icon>{{ icon }}</v-icon>
  </v-btn>
  <v-btn
    v-else
    :color="aButtonColor"
    :variant="variant"
    :size="size"
    :loading="loading"
  >
    {{ text }}
  </v-btn>
</template>

<script lang="ts">
export type AButtonColors =
  | "base"
  | "blue"
  | "purple"
  | "green"
  | "red"
  | "yellow";
export type AButtonSizes =
  | "x-small"
  | "small"
  | "default"
  | "large"
  | "x-large";
export type AButtonVariants =
  | "text"
  | "flat"
  | "elevated"
  | "tonal"
  | "outlined"
  | "plain"
  | "radio";
</script>

<script lang="ts" setup>
import { usePreferredColorScheme } from "@vueuse/core";
import { PropType, defineProps, computed } from "vue";
import { useTheme } from "vuetify";

const props = defineProps({
  color: {
    type: String as PropType<AButtonColors>,
    default: "base",
  },
  variant: {
    type: String as PropType<AButtonVariants>,
    default: "flat",
  },
  size: {
    type: String as PropType<AButtonSizes>,
    default: "default",
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
    default: false,
  },
});

const theme = useTheme();
const preferredColor = usePreferredColorScheme();

const inDarkMode = computed(() => {
  return theme.global.current.value.dark || preferredColor.value === 'dark';
});

const aButtonColor = computed(() => {
  if (props.disabled) {
    return inDarkMode.value ? "#444445" : "#E4E7E9";
  }

  switch (props.color) {
    case "base":
      if (props.variant === "outlined" || props.variant === "text") {
        return "#6B6C6D";
      }
      return inDarkMode.value ? "#202121" : "#F7F9FA";
    case "blue":
      return inDarkMode.value ? "#1E3A8A" : "#85C1E9"; // Azul en modo oscuro
    case "purple":
      return inDarkMode.value ? "#5B21B6" : "#AF7AC5";
    case "green":
      return inDarkMode.value ? "#166534" : "#65D740";
    case "red":
      return inDarkMode.value ? "#B91C1C" : "#FF4040";
    case "yellow":
      if (props.variant === "outlined" || props.variant === "text") {
        return inDarkMode.value ? "#854D0E" : "#C37500";
      }
      return inDarkMode.value ? "#D97706" : "#F4D03F";
    default:
      return inDarkMode.value ? "#202121" : "#F7F9FA"; // Valor por defecto en modo oscuro
  }
});
</script>

<style scoped>
:not(:disabled).a-button-blue,
:not(:disabled).a-button-purple,
:not(:disabled).a-button-green,
:not(:disabled).a-button-red {
  color: #ffffff;
}
</style>
