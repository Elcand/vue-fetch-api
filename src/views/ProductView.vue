<script setup>
import { onMounted, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
import ProductForm from "@/components/ProductForm.vue";

const route = useRoute();
const router = useRouter();
const id = route.params.id;
const product = ref({});
const loading = ref(true);
const API_URL = `http://localhost:3000/products/${id}`;

onMounted(async () => {
  try {
    const res = await axios.get(API_URL);
    product.value = res.data;
  } catch (err) {
    console.error("Gagal mengambil data:", err);
  } finally {
    loading.value = false;
  }
});

async function deleteProduct() {
  try {
    await axios.delete(API_URL);
    router.push("/");
  } catch (err) {
    console.error("Gagal menghapus data:", err);
  }
}
</script>

<template>
  <div class="container">
    <div v-if="loading" class="loading">
      <div class="spinner"></div>
      <p>Memuat data...</p>
    </div>

    <div v-else class="product-detail">
      <ProductForm />
      <!-- Product Card -->
      <div class="product-card">
        <div class="image-container">
          <!-- Tombol Back di dalam gambar (pojok kiri atas) -->
          <router-link to="/" class="back-link-floating">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M19 12H5M12 19l-7-7 7-7" />
            </svg>
            Kembali
          </router-link>

          <img
            :src="product.image"
            :alt="product.title"
            class="product-image"
          />
        </div>

        <div class="product-info">
          <h1 class="product-title">{{ product.title }}</h1>

          <div class="price-tag">
            <span class="currency">Rp</span>
            <span class="price">{{
              product.price?.toLocaleString("id-ID")
            }}</span>
          </div>

          <div class="description-section">
            <h3>Deskripsi Produk</h3>
            <p class="product-description">{{ product.description }}</p>
          </div>

          <!-- Floating buttons di kanan bawah -->
          <div class="floating-buttons">
            <button class="btn-float btn-primary">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="18"
                height="18"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"
                />
                <line x1="7" y1="7" x2="7.01" y2="7" />
              </svg>
              <span>Edit</span>
            </button>
            <button class="btn-float btn-danger" @click="deleteProduct">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="18"
                height="18"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <polyline points="3 6 5 6 21 6" />
                <path
                  d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"
                />
                <line x1="10" y1="11" x2="10" y2="17" />
                <line x1="14" y1="11" x2="14" y2="17" />
              </svg>
              <span>Hapus</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

.container {
  max-width: 850px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
}

.loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 400px;
  color: #00b894;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 4px solid rgba(102, 126, 234, 0.2);
  border-top-color: #00b894;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.product-card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
  animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.image-container {
  position: relative;
  background: linear-gradient(135deg, #f5f7fa 0%, #e8ecf1 100%);
  display: flex;
  justify-content: center;
}

/* Tombol Back mengambang di pojok kiri atas gambar */
.back-link-floating {
  position: absolute;
  top: 20px;
  left: 20px;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 18px;
  background: #00b894;
  backdrop-filter: blur(10px);
  color: white;
  text-decoration: none;
  border-radius: 12px;
  font-weight: 600;
  font-size: 14px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  z-index: 10;
}

.back-link-floating:hover {
  background: #008c70;
  transform: translateX(-5px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

.product-image {
  max-width: 100%;
  max-height: 100%;
  transition: transform 0.3s ease;
}

.product-image:hover {
  transform: scale(1.03);
}

.product-info {
  padding: 50px 40px;
  display: flex;
  flex-direction: column;
  gap: 25px;
  position: relative;
}

.product-title {
  font-size: 32px;
  font-weight: 700;
  color: #2d3748;
  margin: 0;
  line-height: 1.3;
}

.price-tag {
  display: inline-flex;
  align-items: baseline;
  gap: 5px;
  width: fit-content;
}

.currency {
  font-size: 18px;
  font-weight: 600;
  color: #4a5568;
}

.price {
  font-size: 36px;
  font-weight: 700;
  color: #00b894;
}

.description-section {
  flex: 1;
}

.description-section h3 {
  font-size: 18px;
  font-weight: 600;
  color: #4a5568;
  margin: 0 0 15px 0;
}

.product-description {
  font-size: 16px;
  line-height: 1.8;
  color: #718096;
  margin: 0;
}

/* Floating buttons di kanan/end */
.floating-buttons {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 12px;
  margin-top: auto;
  padding-top: 20px;
}

.btn-float {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  font-size: 14px;
  font-weight: 600;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.btn-float span {
  display: inline-block;
}

.btn-float:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

.btn-float:active {
  transform: translateY(0);
}

.btn-float.btn-primary {
  background: linear-gradient(135deg, #00b894 0%, #764ba2 100%);
  color: white;
}

.btn-float.btn-primary:hover {
  box-shadow: 0 6px 16px rgba(102, 126, 234, 0.4);
}

.btn-float.btn-danger {
  background: linear-gradient(135deg, #f56565 0%, #c53030 100%);
  color: white;
}

.btn-float.btn-danger:hover {
  box-shadow: 0 6px 16px rgba(245, 101, 101, 0.4);
}

/* Responsive Design */
@media (max-width: 968px) {
  .product-card {
    grid-template-columns: 1fr;
  }

  .image-container {
    min-height: 400px;
    padding: 60px 30px 30px 30px;
  }

  .back-link-floating {
    top: 15px;
    left: 15px;
    padding: 8px 14px;
    font-size: 13px;
  }

  .product-info {
    padding: 30px 25px;
  }

  .product-title {
    font-size: 26px;
  }

  .price {
    font-size: 30px;
  }

  .floating-buttons {
    gap: 10px;
  }

  .btn-float {
    padding: 10px 18px;
    font-size: 13px;
  }
}

@media (max-width: 576px) {
  .container {
    padding: 10px;
  }

  .image-container {
    padding: 60px 20px 20px 20px;
  }

  .back-link-floating {
    padding: 8px 12px;
    font-size: 12px;
    gap: 6px;
  }

  .back-link-floating svg {
    width: 16px;
    height: 16px;
  }

  .product-info {
    padding: 25px 20px;
  }

  .product-title {
    font-size: 22px;
  }

  .price {
    font-size: 26px;
  }

  .floating-buttons {
    flex-direction: column;
    gap: 8px;
  }

  .btn-float {
    width: 100%;
    justify-content: center;
  }

  .btn-float span {
    display: inline-block;
  }
}
</style>
