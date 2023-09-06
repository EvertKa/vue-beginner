<script setup>
import { onMounted, ref } from 'vue';
import { fakeAPI } from '../api/fakeAPI';

const products = ref(null);

onMounted( async () => {

  try {
    products.value = await fakeAPI.get('/products')
  } catch(error) {
    console.log(error);
    throw new Error(error);
  }

});
</script>

<template>
  <article v-for="product in products?.data" :key="product.id">
    <img :src="product.image" alt="">
    <h4>{{ product.title }}</h4>
    <p>{{ product.description }}</p>
  </article>
</template>