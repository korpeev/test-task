<script lang="ts" setup>

</script>
<template>
  <header class="header" :class="{'with-background': $route.path !== '/'}">
    <h1 class="logo">Logo</h1>
    <nav class="nav">
      <ul class="nav-list">
        <li class="nav-list-item">
          <nuxt-link to="/">Main</nuxt-link>
        </li>
        <li class="nav-list-item">
          <nuxt-link to="/about-us">About Us</nuxt-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background: transparent;
  color: white;
  border-radius: 12px;
  &.with-background {
    background: white;
    color: black;
    .nav-list-item {
      a {
        color: black;
      }
    }
  }
  .logo {
    margin: 0;
    font-size: 28px;
    font-family: Roboto, sans-serif;
  }
}
.nav {
  &-list {
    display: flex;
    gap: 10px;
    &-item {
      list-style: none;
      a {
        color: white;
      }
    }
  }
}
</style>