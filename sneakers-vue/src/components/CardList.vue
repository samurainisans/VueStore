<script setup>
import Card from './Card.vue'

const onClickAdd = () => {
  alert('Добавлено')
}

defineProps({
  items: {
    type: Array,
    default: () => []
  }
})
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :price="item.price"
      :title="item.title"
      :image-url="item.imageUrl"
      :on-click-add="onClickAdd"
    />
  </div>
</template>
