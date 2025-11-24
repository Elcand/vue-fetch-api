<script setup>
const props = defineProps({
  page: Number,
  totalPages: Number,
});

const emit = defineEmits(["change-page"]);

function changePage(newPage) {
  emit("change-page", newPage);
}
</script>

<template>
  <button
    class="pagination-button"
    @click="changePage(page - 1)"
    @show="page > 1"
    id="prevPage"
  >
    &lt;
  </button>
  <span class="pagination-current-page">Page {{ page }}</span>
  <button
    class="pagination-button"
    @click="changePage(page + 1)"
    @show="page < totalPages"
    id="nextPage"
  >
    &gt;
  </button>
</template>

<script></script>

<style scoped>
.pagination-button {
  background-color: #fff;
  color: #00b894;
  padding: 8px 12px;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  font-size: 16px;
  margin: 0 5px;
}
</style>
