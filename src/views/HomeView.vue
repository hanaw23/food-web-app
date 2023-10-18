<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import CardProduct from "../components/CardProduct.vue";

const products = ref([]);
const pagination = ref({
  page: 1,
  limit: 3,
  length: 0,
});

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
    .then((response) => {
      products.value = JSON.parse(response.data);
      pagination.value.length += 3;
    })
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
      products.value = JSON.parse(response.data);
      pagination.value.length += 3;
    })
    .catch((error) => console.log(error));
};

const loadPrevious = async () => {
  const urlWebProducts = `http://localhost:3000/products?_page=${(pagination.value.page -= 1)}&_limit=${pagination.value.limit}`;
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
};
</script>

<template>
  <div class="main-container">
    <div class="title">
      <div>
        <h2>Recomended <strong>Foods</strong> This Week</h2>
      </div>
    </div>

    <div class="grid-products">
      <div v-for="product in products" :key="product.id">
        <CardProduct :product="product" />
      </div>
    </div>

    <div class="btn-container">
      <div>
        <button v-if="pagination.length !== pagination.limit" class="btn-preview" type="button" @click="loadPrevious">Preview</button>
        <div v-else />
      </div>

      <p>Page {{ pagination.page }} of 3</p>

      <div>
        <button v-if="pagination.length !== 9" type="button" class="btn-next" @click="loadMore">Next</button>
        <div v-else />
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  margin-top: 2rem;
  margin-bottom: 2rem;
  margin-left: auto;
  margin-right: auto;
}
.title {
  margin-bottom: 2rem;
}
.grid-products {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

.btn-container {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
  margin-bottom: 2rem;
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
  background-color: #0a5793;
  color: #ffffff;
}

.dot {
  height: 0.5rem;
  width: 0.5rem;
  background-color: #fcf6f6;
  border-radius: 50%;
  display: inline-block;
  margin-left: 0.5rem;
  margin-right: 0.5rem;
}
</style>
