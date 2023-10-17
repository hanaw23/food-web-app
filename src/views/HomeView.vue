<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import CardProduct from "../components/CardProduct.vue";

const products = ref([]);
const pagination = ref({
  page: 1,
  limit: 3,
});
const disabledLoadMore = ref(false);

// Fetch data from API
onMounted(async () => {
  getProductMethods();
});
const getProductMethods = async () => {
  axios({
    method: "get",
    url: "http://localhost:3000/products?_page=1&_limit=3",
    responseType: "stream",
  })
    .then((response) => (products.value = JSON.parse(response.data)))
    .catch((error) => console.log(error));
};

const loadMore = async () => {
  const urlWebProducts = `http://localhost:3000/products?_page=${(pagination.value.page += 1)}&_limit=${pagination.value.limit}`;
  axios({
    method: "get",
    url: urlWebProducts,
    responseType: "stream",
  })
    .then((response) => {
      if (JSON.parse(response.data).length === 0) {
        disabledLoadMore.value = true;
      } else {
        products.value.push(...JSON.parse(response.data));
      }
    })
    .catch((error) => console.log(error));
};
</script>

<template>
  <div>
    <div class="row mt-4">
      <div class="col">
        <h2>Best <strong>Foods</strong></h2>
      </div>
      <div class="col">
        <RouterLink to="/foods" class="btn btn-success float-right">View all</RouterLink>
      </div>
    </div>

    <div class="row mb-3">
      <div v-for="product in products" :key="product.id">
        <CardProduct :product="product" />
      </div>
      <button type="button" class="btn btn-primary" :disabled="disabledLoadMore" @click="loadMore">Load More</button>
    </div>
  </div>
</template>
