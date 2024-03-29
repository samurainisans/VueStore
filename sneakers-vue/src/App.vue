<script setup>
import { onMounted, provide, reactive, ref, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const loadData = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(`https://bb957a3e7ec47e7e.mokky.dev/items`, { params })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false
    }))
  } catch (error) {
    console.error('Ошибка загрузки данных:', error)
  }
}

const loadFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://bb957a3e7ec47e7e.mokky.dev/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)

      if (!favorite) {
        return item
      }

      return { ...item, isFavorite: true, favoriteId: favorite.id }
    })
  } catch (error) {
    console.error('Ошибка загрузки данных:', error)
  }
}

const addToFavorite = async (item) => {
  item.isFavorite = !item.isFavorite
  console.log(item)

  if (item.isFavorite) {
    try {
      await axios.post(`https://bb957a3e7ec47e7e.mokky.dev/favorites`, {
        parentId: item.id
      })
    } catch (error) {
      console.error('Ошибка загрузки данных:', error)
    }
  } else {
    try {
      await axios.delete(`https://bb957a3e7ec47e7e.mokky.dev/favorites/${item.favoriteId}`)
    } catch (error) {
      console.error('Ошибка загрузки данных:', error)
    }
  }
}

onMounted(async () => {
  await loadData()
  await loadFavorites()
})
watch(() => ({ ...filters }), loadData, { deep: true })

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

provide('addToFavorite', addToFavorite)
</script>

<template>
  <div>
    <Drawer />
    <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
      <Header />

      <div class="p-10">
        <div class="flex justify-between items-center">
          <h2 class="text-3xl font-bold mb-5">Все кроссовки</h2>

          <div class="flex gap-4">
            <select
              class="bg-white py-2 px-3 border rounded-md outline-none"
              @change="onChangeSelect"
            >
              <option value="name">По названию</option>
              <option value="price">По цене (дешевые)</option>
              <option value="-price">По цене (дорогие)</option>
            </select>

            <div class="relative">
              <img class="absolute left-3 top-2.5" src="/search.svg" alt="search" />
              <input
                class="border rounded-md p-1.5 pl-10 pr-4 outline-none focus:border-gray-400"
                @input="onChangeSearchInput"
                placeholder="Поиск..."
              />
            </div>
          </div>
        </div>
        <div class="mt-10">
          <CardList :items="items" @addToFavorite="addToFavorite" />
        </div>
      </div>
    </div>
  </div>
</template>
