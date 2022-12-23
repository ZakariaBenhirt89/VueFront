<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <a class="mt-5" href="#" target="_blank">
      <img src="https://res.cloudinary.com/dy6vgsgr8/image/upload/v1671734071/329359_kkywj6.png" class="logo" alt="Vite logo" />
    </a>
    <h1 class="text-3xl font-bold underline">
    Assessment
  </h1>
  </div>
  <HelloWorld id="container" class="mt-5" msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 0.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
