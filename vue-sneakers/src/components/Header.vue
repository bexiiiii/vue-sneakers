<!-- src/components/Header.vue -->
<template>
    <header class="flex justify-between border-b border-slate-200 px-10 py-8">
      <div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue sneakers</h2>
          <p class="text-slate-500">The Shop of best sneakers</p>
        </div>
      </div>
  
      <ul class="flex items-center gap-10">
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/cart.svg" alt="cart" />
          <b>1208 kzt</b>
        </li>
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="heart" />
          <span>Закладки</span>
        </li>
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/profile.svg" alt="profile" />
          <span>Профиль</span>
        </li>
      </ul>
    </header>
  </template>
  
  <script setup>
  // можно оставить пустым, если не используешь логику
  </script>
  