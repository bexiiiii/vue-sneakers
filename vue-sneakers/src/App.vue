<script setup>
import Header from './components/Header.vue';
import CartList from './components/CartList.vue';
import Drawer from './components/Drawer.vue';
import { onMounted, ref, watch, reactive, provide } from 'vue';
import axios from 'axios';

// Массив для хранения товаров
const items = ref([]);

// Объект для фильтров (сортировка и поиск)
const filters = reactive({
  sortBy: '',
  searchQuery: ''
});

const fetchFavorites = async () => {
  try {
    
    // Отправляем GET-запрос на сервер
    const { data: favourites } = await axios.get(`https://b79d33b5b3d9e0a4.mokky.dev/favourites`)
    items.value = items.value.map(item =>{
      const favourite = favourites.find(fav => favourite.parentId === item.id);
      if (favourite) {
        return {
          ...item,
          isFavorite: true,
          favouriteId: favourite.id,
        }
      }
      return item;
    });
  } catch (error) {
    console.error(error);
  }
};

const addToFavourites = async (item) => {
  try {
    // Отправляем POST-запрос на сервер
    const { data } = await axios.post(`https://b79d33b5b3d9e0a4.mokky.dev/favourites`, {
      parentId: item.id,
      imageUrl: item.imageUrl,
      title: item.title,
      price: item.price,
    });
    items.value = items.value.map(obj => {
      if (obj.id === item.id) {
        return {
          ...obj,
          isFavorite: true,
          favouriteId: data.id,
        }
      }
      return obj;
    });
  } catch (error) {
    console.error(error);
  }
};


const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    };
    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`;

    }
    // Отправляем GET-запрос на сервер
    const { data } = await axios.get(`https://604781a0efa572c1.mokky.dev/items`, {
      params
    });
    items.value = data.map(obj=> ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }));
  } catch (error) {
    console.error(error);
  }
};

// Загружаем данные при монтировании
onMounted(async() => {
  await fetchItems();
  await fetchFavorites();
});

// Наблюдаем за изменениями в сортировке
watch(filters, fetchItems);

provide('addFavourite', addToFavourite);

// Обработчик для изменения фильтров сортировки
const onChangeSelect = (event) => {
  filters.sortBy = event.target.value;
};

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value;
};
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold">All sneakers</h2>

        <div class="flex gap-4">
          <!-- Выпадающий список сортировки -->
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">From name</option>
            <option value="price">From price</option>
            <option value="rating">From rating</option>
            <option value="date">From date</option>
            <option value="popularity">From popularity</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="search">
            <input 
            @input="onChangeSearchInput"
            class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400" type="text" placeholder="Search..." />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <!-- Передаем данные о товарах в CartList -->
        <CartList :items="items" />
      </div>
    </div>
  </div>
</template>
