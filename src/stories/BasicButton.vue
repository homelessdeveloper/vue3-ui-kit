<template>
  <button type="button" class="bg-red-500" @click="onClick" :style="style">
    {{ label }}
  </button>
</template>

<script setup lang="ts">
import { Size } from "@/types/Size";
import { computed } from "vue";

interface Props {
  label: string;
  primary?: boolean;
  backgroundColor?: string;
  size: Size;
}

interface Emits {
  (event: "click"): void;
}

const props = withDefaults(defineProps<Props>(), { primary: false });

const emit = defineEmits<Emits>();

const onClick = () => {
  emit("click");
};

const classes = computed(() => ({
  "storybook-button": true,
  "storybook-button--primary": props.primary,
  "storybook-button--secondary": !props.primary,
  [`storybook-button--${props.size || "medium"}`]: true,
}));

const style = computed(() => ({
  backgroundColor: props.backgroundColor,
}));
</script>

<style lang="scss" scoped>
.storybook-button {
  font-family: "Overpass", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-weight: 700;
  border: 0;
  border-radius: 3rem;
  cursor: pointer;
  display: inline-block;
  line-height: 1;
  transition: all 0.15s ease-in-out;
}

.storybook-button--small {
  font-size: 12px;
  padding: 10px 16px;
}

.storybook-button--medium {
  font-size: 14px;
  padding: 11px 20px;
}

.storybook-button--large {
  font-size: 16px;
  padding: 12px 24px;
}
</style>
