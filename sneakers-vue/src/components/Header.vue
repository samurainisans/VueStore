<template>
  <header class="flex justify-between border-b border-slate-300 py-8 px-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-2xl font-bold uppercase">Vue Sneakers</h2>
        <p class="text-slate-400">Магазин кросовок</p>
      </div>
    </div>
    <ul class="flex gap-10 items-center text-slate-400">
      <li class="flex gap-3 items-center hover:text-slate-600 cursor-pointer">
        <img src="/cart.svg" alt="Cart" />
        <b>1205 руб.</b>
      </li>

      <li class="flex gap-3 items-center hover:text-slate-600 cursor-pointer">
        <img src="/heart.svg" alt="Heart" />
        <span>Закладки</span>
      </li>

      <li class="flex gap-3 items-center hover:text-slate-600 cursor-pointer">
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
