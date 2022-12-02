<script setup>
const props = defineProps(["img", "title", "price"])
</script>

<template>
  <div class="text-center h-80 bg-gray-50 p-2">
    <figure class="relative overflow-hidden w-full h-36 mb-5">
      <img class="blur absolute object-cover w-full h-36" :src="img" alt="" />
      <img class="absolute object-contain w-full h-36" :src="img" alt="" />
    </figure>
    <h2 class="my-2 line-clamp-3 h-20">{{ title }}</h2>
    <span class="my-2 text-cyan-500 text-lg font-bold">${{ price }}</span>
  </div>
</template>

<style>
.line-clamp-3 {
  line-clamp: 3;
}
</style>