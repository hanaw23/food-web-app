<script setup>
defineProps({
  product: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="card">
    <img :src="`assets/images/${product.gambar}`" class="card-img-top" alt="assets/images/default.png" />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <div class="card-price-container">
        <span class="card-price"> Rp. {{ product.harga }}, -</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 18rem;
  border: 1px solid #fcf6f6;
  box-shadow: 5px 5px 5px 1px rgba(0, 0, 0, 0.125);
  border-radius: 15px;
}

.card-img-top {
  width: 100%;
  height: 15vw;
  object-fit: cover;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}

.card-title {
  font-size: 20px;
  font-weight: bold;
  line-height: 1.2;
  margin-bottom: 2rem;
  margin-top: -0.5rem;
  color: #494646;
}

.card-body {
  padding: 1.25rem;
}

.card-price-container {
  font-size: 0.875rem;
  margin-bottom: 0.75rem;
}

.card-price {
  font-size: 12px;
  color: #8a8d8f;
  font-weight: bold;
}
</style>
