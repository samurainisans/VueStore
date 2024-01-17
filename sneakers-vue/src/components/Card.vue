<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function
})
</script>

<template>
  <div>
    <div
      class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:shadow-xl hover:border-slate-200 transition duration-130 ease-in hover:scale-105 hover:shadow-2xl"
    >
      <img
        :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
        alt="like-2"
        class="absolute top-8 left-8"
        @click="onClickFavorite"
      />

      <img :src="imageUrl" alt="Sneaker" />
      <p class="mt-2">{{ title }}</p>
      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-400">Цена</span>
          <span>
            <b>{{ price }} руб.</b>
          </span>
        </div>
        <img alt="plus" :src="!isAdded ? '/plus.svg' : '/checked.svg'" @click="onClickAdd" />
      </div>
    </div>
  </div>
</template>
