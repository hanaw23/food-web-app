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
      <!-- <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
      <a href="#" class="btn btn-primary">Go somewhere</a> -->
    </div>
  </div>
</template>
