<script setup lang="ts">
import HomeView from "./views/HomeView.vue";
</script>

<template>
  <!-- <RouterLink to="/">Home</RouterLink>
  <RouterLink to="/about">About</RouterLink>
  <RouterView />-->
  <Suspense>
    <template #default> <HomeView /> </template>
    <template #fallback> Loading... </template>
  </Suspense>
</template>

<style scoped></style>
