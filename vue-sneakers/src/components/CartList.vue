<script setup>
import Cart from './cart.vue';

const onClickAdd = () => {
    alert('add');
}

defineProps({
    items: Array,
})
</script>

<template>
  <div class="grid grid-cols-4 gap-5 mb-10">
    <!-- Используем v-for для перебора items -->
    <Cart 
      v-for="item in items" 
      :key="item.id" 
      :title="item.title" 
      :image-url="item.imageUrl" 
      :price="item.price"
      :onClickAdd="onClickAdd" 
      :is-favorite="item.isFavorite"
    />
  </div>
</template>
