<script lang="ts" setup>
const copyright = new Date().getFullYear()
</script>
<template>
  <footer class="footer">
    <span>copyright {{copyright}}</span>
  </footer>
</template>
<style lang="scss" scoped>
.footer {
  padding: 20px 0;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top: 1px solid white;
}
</style>