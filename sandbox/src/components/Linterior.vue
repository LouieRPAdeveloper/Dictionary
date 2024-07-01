<script setup lang="ts">
import { ref } from "vue";

defineProps<{ pao: string }>();
</script>

<template>
  <p class="d-flex justify-content-start text-start">* {{ pao }}</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
* {
  margin: 0px;
  padding: 0px;
  font-size: 22px;
}
</style>
