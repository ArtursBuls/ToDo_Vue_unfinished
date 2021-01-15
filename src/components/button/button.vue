<template>
  <button >
    {{ label }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Button = defineComponent({
  props: {
    label: String,
  },
});

export default Button;
</script>

<style src="./button.scss" lang="scss" scoped></style>
