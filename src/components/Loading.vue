<template>
  <div class="loading-container">
    <div class="dots-wrapper">
      <div class="dot dot-1"></div>
      <div class="dot dot-2"></div>
      <div class="dot dot-3"></div>
    </div>
    <p class="loading-text">Sedang memproses...</p>
  </div>
</template>

<script>
export default {
  name: "Loading",
};
</script>

<style scoped>
.loading-container {
  text-align: center;
}

.dots-wrapper {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  justify-content: center;
}

.dot {
  width: 16px;
  height: 16px;
  background-color: #bdbcc3;
  border-radius: 50%;
  animation: bounce 0.6s infinite alternate;
}

.dot-1 {
  animation-delay: 0s;
}

.dot-2 {
  animation-delay: 0.1s;
}

.dot-3 {
  animation-delay: 0.2s;
}

.loading-text {
  color: #4b5563;
  font-size: 18px;
  margin: 0;
}

@keyframes bounce {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-12px);
  }
}
</style>
