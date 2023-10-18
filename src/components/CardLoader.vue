<script setup></script>
<template>
  <div class="card">
    <div class="skeleton-loader-image" />
    <div class="card-body">
      <h5 class="skeleton-loader-title" />
      <div class="skeleton-loader" />
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 18rem;
  border: 1px solid #fcf6f6;
  box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.125);
  border-radius: 15px;
}

.card-body {
  padding: 1.25rem;
}

.skeleton-loader {
  width: 100%;
  display: block;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.5) 50%, rgba(255, 255, 255, 0) 80%), lightgray;
  background-repeat: repeat-y;
  background-size: 50px 500px;
  background-position: 0 0;
  animation: shine 1s infinite;
}

.skeleton-loader-title {
  width: 100%;
  height: 2rem;
  margin-bottom: 2rem;
  margin-top: -0.5rem;
  display: block;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.5) 50%, rgba(255, 255, 255, 0) 80%), lightgray;
  background-repeat: repeat-y;
  background-size: 50px 500px;
  background-position: 0 0;
  animation: shine 1s infinite;
}

.skeleton-loader-image {
  width: 100%;
  height: 10rem;
  margin-bottom: 2rem;
  margin-top: -0.5rem;
  display: block;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.5) 50%, rgba(255, 255, 255, 0) 80%), lightgray;
  background-repeat: repeat-y;
  background-size: 50px 500px;
  background-position: 0 0;
  animation: shine 1s infinite;
}

@keyframes shine {
  to {
    background-position: 100% 0, /* move highlight to right */ 0 0;
  }
}

.skeleton-loader:empty {
  width: 100%;
  height: 15px;
  display: block;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.5) 50%, rgba(255, 255, 255, 0) 80%), lightgray;
  background-repeat: repeat-y;
  background-size: 50px 500px;
  background-position: 0 0;
  animation: shine 1s infinite;
}
</style>
