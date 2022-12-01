<script setup>
import { reactive, ref, watch } from 'vue';

const searchTerm = ref('');
const products = ref([]);

const findProducts = async term => {
  if (term) {
  fetch(`https://dummyjson.com/products/search?q=${term}`)
    .then(res => res.json())
    .then(data => {
      products.value = data.products
    });
  } else {
    products.value = [];
  }
};

watch(searchTerm, newTerm => findProducts(newTerm));
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input type="text" class="p-2 border-2 border-gray-dark" v-model="searchTerm" placeholder="Start typing..." />
    <ul class="list-disc">
      <li v-for="product in products">{{product.title}}</li>
    </ul>
  </div>
</template>
