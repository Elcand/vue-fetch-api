<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";

const route = useRoute();
const id = route.params.id;
const product = ref({});

onMounted(async () => {
  const API_URL = `http://localhost:3000/products/${id}`;
  try {
    const res = await axios.get(API_URL);
    product.value = res.data;
  } catch (err) {
    console.error("Gagal mengambil data:", err);
  }
});
</script>

<template>
  <div class="product-detail">
    <h2>{{ product.title }}</h2>
    <img :src="product.image" :alt="product.name" class="product-image" />
    <p>{{ product.description }}</p>
    <p>Rp {{ product.price }}</p>
    <router-link to="/" class="back-button">Back</router-link>
  </div>
</template>

<style scoped>
.product-detail {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  text-align: center;
}

.product-image {
  max-width: 100%;
  height: auto;
  margin-bottom: 10px;
}

.product-detail p {
  margin-bottom: 5px;
}

.product-detail button {
  margin-top: 10px;
  padding: 10px 20px;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.back-button {
  display: inline-block;
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.back-button:hover {
  background-color: #0056b3;
}

.delete-button {
  display: inline-block;
  padding: 8px 16px;
  background-color: #ff0000;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.delete-button:hover {
  background-color: #b30000;
}
</style>
