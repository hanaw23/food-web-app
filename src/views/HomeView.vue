<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

import CardProduct from "../components/CardProduct.vue";
import CardLoader from "../components/CardLoader.vue";
import Hero from "../components/Hero.vue";

// ==== VARIABLES ====
const products = ref([]);
const pagination = ref({
  page: 1,
  limit: 3,
  length: 0,
});
const loading = ref(false);

// ==== METHODS ====
// Fetch data from API
onMounted(async () => {
  getProductMethods();
});
const getProductMethods = async () => {
  loading.value = true;
  axios({
    method: "get",
    url: "https://my-json-server.typicode.com/hanaw23/food-data/products?_page=1&_limit=3",
    responseType: "stream",
  })
    .then((response) => {
      products.value = JSON.parse(response.data);
      pagination.value.length += 3;
    })
    .catch((error) => console.log(error));
  loading.value = false;
};

const loadMore = async () => {
  loading.value = true;
  const urlWebProducts = `https://my-json-server.typicode.com/hanaw23/food-data/products?_page=${(pagination.value.page += 1)}&_limit=${pagination.value.limit}`;
  axios({
    method: "get",
    url: urlWebProducts,
    responseType: "stream",
  })
    .then((response) => {
      products.value = JSON.parse(response.data);
      pagination.value.length += 3;
    })
    .catch((error) => console.log(error));
  loading.value = false;
};

const loadPrevious = async () => {
  loading.value = true;
  const urlWebProducts = `https://my-json-server.typicode.com/hanaw23/food-data/products?_page=${(pagination.value.page -= 1)}&_limit=${pagination.value.limit}`;
  axios({
    method: "get",
    url: urlWebProducts,
    responseType: "stream",
  })
    .then((response) => {
      products.value = JSON.parse(response.data);
      pagination.value.length -= 3;
    })
    .catch((error) => console.log(error));
  loading.value = false;
};
</script>

<template>
  <div>
    <Hero />

    <div class="main-container">
      <div class="title">
        <div class="recomended-title">Recommended Foods This Week</div>
      </div>

      <div class="grid-products">
        <div v-for="product in products" :key="product.id">
          <CardLoader v-if="loading" />
          <CardProduct v-else :product="product" />
        </div>
      </div>

      <div class="btn-container">
        <div>
          <button v-if="pagination.length !== pagination.limit" class="btn-preview" type="button" @click="loadPrevious">Preview</button>
          <div v-else />
        </div>

        <small class="paginator">page {{ pagination.page }} of 3</small>

        <div>
          <button v-if="pagination.length !== 9" type="button" class="btn-next" @click="loadMore">Next</button>
          <div v-else />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  margin: auto;
  margin-top: 5rem;
}
.title {
  margin-bottom: 2rem;
}
.grid-products {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
  padding-left: 10rem;
  padding-right: 10rem;
}

.recomended-title {
  padding-left: 10rem;
  padding-right: 10rem;
  color: #494646;
  font-size: 20px;
  font-weight: 700;
}

.btn-container {
  display: flex;
  justify-content: space-between;
  margin-top: 55px;
  padding-left: 10rem;
  padding-right: 16rem;
}

button {
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  border: 1px solid #fcf6f6;
  font-weight: bold;
  cursor: pointer;
}
.btn-preview {
  background-color: #858080;
  color: #ffffff;
}

.btn-next {
  background-color: #97bc78;
  color: #ffffff;
}
:hover.btn-next {
  background-color: #6f8859;
}
:hover.btn-preview {
  background-color: #414040;
}
.paginator {
  color: #b3adad;
}
</style>
