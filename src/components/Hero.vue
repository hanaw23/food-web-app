<script setup></script>

<template>
  <div class="container-hero">
    <div class="container-text">
      <h1 class="title">Welcome to Foody Mart</h1>
      <p class="description">What are you going to eat today?</p>
    </div>
    <img src="assets/images/ilustrasi.png" alt="hero" class="logo" />
  </div>
</template>

<style scoped>
.container-text {
  width: 25%;
  padding-left: 2rem;
}
.description {
  font-size: 25px;
  margin-bottom: 2rem;
  color: #a4a1a1;
}
.title {
  font-size: 55px;
  font-weight: bold;
  margin-bottom: 2rem;
  color: #89a86e;
}
.container-hero {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10rem;
  width: 100%;
  background-image: linear-gradient(to right, #ffffff, #97bc78);
}
.logo {
  width: 50%;
  height: 20%;
  object-fit: cover;
}
</style>
