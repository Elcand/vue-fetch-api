<script setup lang="ts">
import HomeView from "./views/HomeView.vue";
</script>

<template>
  <Suspense>
    <template #default>
      <HomeView />
    </template>
    <template #fallback> Loading... </template>
  </Suspense>
</template>

<style scoped></style>
