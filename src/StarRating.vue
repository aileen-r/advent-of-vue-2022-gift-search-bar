<script setup>
import { computed } from 'vue';
const props = defineProps(["rating"]);
const percentageFilled = computed(() => `${(props.rating / 5) * 100}%`)
const title = computed(() => `Rated ${props.rating} out of 5 stars`)
</script>

<template>
  <i class="star-rating" :title="title" />
</template>

<style scoped>
/* Thanks to https://codepen.io/4m6/pen/wvqEzEr */
.star-rating {
  text-align: left;
  font-style: normal;
  display: inline-block;
  position: relative;
  unicode-bidi: bidi-override;
}

.star-rating::before {
  display: block;
  content: '★★★★★';
  color: #ddd;
}

.star-rating::after {
  white-space: nowrap;
  position: absolute;
  top: 0;
  left: 0;
  content: '★★★★★';
  width: v-bind(percentageFilled);
  color: orange;
  overflow: hidden;
  height: 100%;
}
</style>