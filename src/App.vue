<script setup>
import { ref, watch } from 'vue';
import Loader from './Loader.vue'
import Product from './Product.vue'

const searchTerm = ref('');
const products = ref([]);
const isLoading = ref(false);
const hasError = ref(false);

const findProducts = async term => {
  if (term) {
    isLoading.value = true;
    hasError.value = false;
    fetch(`https://dummyjson.com/products/search?q=${term}`)
      .then(res => res.json())
      .then(data => {
        products.value = data.products.slice(0, 5)
      })
      .catch(err => {
        console.error(err);
        hasError.value = true;
      })
      .finally(() => {
        isLoading.value = false;
      });
  } else {
    products.value = [];
  }
};

const debounce = (func, timeout = 300) => {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => { func.apply(this, args); }, timeout);
  };
}

watch(searchTerm, debounce(newTerm => findProducts(newTerm)));
</script>

<template>
  <div class="flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold mt-5">Gift Search Bar</h1>
    <input type="text" class="p-2 border-2 border-gray-dark" v-model="searchTerm" placeholder="Start typing..." />
    <div v-if="hasError" class="px-3 pt-1 pb-1.5 bg-red-100 text-red-600">Something went wrong. ☹</div>
    <Loader v-else-if="isLoading" />
    <ul v-else class="list-none grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-3 px-3">
      <li v-for="product in products">
        <Product :img="product.thumbnail" :title="product.title" :price="product.price" :rating="product.rating" />
      </li>
    </ul>
  </div>
</template>
