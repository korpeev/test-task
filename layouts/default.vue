<template>
  <div class="wrapper">
    <core-header/>
    <div class="content">
      <slot/>
    </div>
    <core-footer/>
  </div>
</template>
<style lang="scss" scoped>

.wrapper {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}
.content {
  flex: 1;
}
</style>
