<script setup>
import DrawerHead from './DrawerHead.vue';  // Импортируем компоненты
import CartItem from './CartItem.vue';
import CartLisItem from './CartLisItem.vue';
</script>

<template>
  <!-- Затемняющий фон -->
  <div class="fixed top-0 left-0 h-full w-full bg-black opacity-70 z-10"></div>

  <!-- Основной контейнер с белым фоном -->
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <!-- Контент модального окна -->
    <DrawerHead />

    <!-- Карточки с товарами -->
    
    <CartLisItem />

    <!-- Прочие элементы -->
    <div class="flex flex-col gap-4 mt-7">
      <!-- Общая сумма -->
      <div class="flex gap-2">
        <span>All</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12999 tenge</b>
      </div>

      <!-- Плата за услуги -->
      <div class="flex gap-4 mt-4">
        <span>Fee 5%</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>200 tenge</b>
      </div>

      <!-- Кнопка "Order it" -->
      <button 
      disabled="''"
      class=" mt -4 transition bg-lime-500 w-full rounded-xl py-3 text-white disabled:bg-slate-300 hover:bg-lime-700 cursor-pointer">
        Order it
      </button>
    </div>
  </div>
</template>
