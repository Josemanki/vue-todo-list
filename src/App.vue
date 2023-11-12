<script setup lang="ts">
import { RouterView } from 'vue-router'
import TodoHeader from './components/TodoHeader.vue'
</script>

<script></script>

<template>
  <TodoHeader />
  <RouterView />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400&family=Rubik:wght@300;400;500;700&display=swap');

:root {
  --primary-color: #9a97f3;
  --secondary-color: #818cab;
  --font-color: #e1e1ff;
  --bg-color: #161625;
  --bg-color-alt: #1d1d30;
  --green: #41b080;
}

* {
  font-family: 'Rubik', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

p,
span,
h1,
h2,
h3,
h4,
h5,
h6,
input,
input::placeholder,
a,
ul,
li {
  color: var(--font-color);
}

body {
  background-color: var(--bg-color);
}

.container {
  max-width: 1100px;
  margin: 0 auto;
}
</style>
