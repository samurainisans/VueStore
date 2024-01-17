<script setup>
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'
</script>

<template>
  <div>
    <div class="fixed top-0 left-0 h-full w-full bg-black/50 z-10"></div>
    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
      <DrawerHead />

      <CartItemList />
      <div class="flex flex-col gap-4 my-6">
        <div class="flex gap-2">
          <span>Итого:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>5000 руб.</b>
        </div>

        <div class="flex gap-2">
          <span>Налог 5%:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>100 руб.</b>
        </div>
      </div>

      <button
        disabled=""
        class="cutsor-pointer disabled:cursor-not-allowed bg-lime-500 text-white w-full rounded-xl disabled:bg-slate-300 p-4 mt-4 hover:bg-lime-600 transition duration-150"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>
ф
