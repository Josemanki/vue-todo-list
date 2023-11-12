<script setup lang="ts">
import { Icon } from '@iconify/vue'
</script>

<template>
  <header>
    <nav class="container">
      <div class="branding">
        <Icon color="#e1e1ff" icon="noto-v1:spiral-notepad" height="2rem" width="2rem"></Icon>
        <h1>Vue Todos</h1>
      </div>
      <ul class="nav-routes">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  background-color: var(--bg-color);

  nav {
    display: flex;
    align-items: center;
    padding: 1rem;

    .branding {
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    h1 {
      font-size: 2rem;
    }

    .nav-routes {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      gap: 0.8rem;
      list-style: none;

      a {
        text-decoration: none;
      }
    }
  }
}
</style>
