<script setup lang="ts">
type DrawerEmits = {
  (event: "update:show", payload: boolean): void;
}
type Props = {
  show?: false;
  direction?: 'left' | 'right' | 'top' | 'bottom'
}
const props = withDefaults(defineProps<Props>(), {
  direction: 'right'
})
const sidebar = ref(false)
const emit = defineEmits<DrawerEmits>()

watch(() => props.show, value => {
  let timer;
  if (value) {
    timer = setTimeout(() => {
      sidebar.value = true
    }, 300)
  } else {
    sidebar.value = false
    clearTimeout(timer)
  }
})
const onClose = () => {
  sidebar.value = false;
  setTimeout(() => {
    emit('update:show', !props.show)
  }, 300)
}
</script>
<template>
  <teleport to="body">
    <transition name="fade">
    <div class="drawer" v-if="show">

      <div @click="onClose"  class="drawer-backdrop"/>

      <transition  :name="`slide-${direction}`">
        <div v-if="sidebar" :style="{
          [direction]: 0,
          height: direction === 'left' || direction === 'right' ? '100vh' : 'auto',
          width: direction === 'left' || direction === 'right' ? '250px' : 'calc(100vw - 32px)',
        }" class="drawer-content">
          <slot/>
        </div>
      </transition>
    </div>
    </transition>
  </teleport>

</template>
<style lang="scss" scoped>
.drawer {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  &-backdrop {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    cursor: pointer;
    z-index: 20;
  }
  &-content {
    background: black;
    position: absolute;
    color: white;
    padding: 20px;
    z-index: 40;
    box-shadow: 0px 5px 10px 2px rgba(255, 255, 255, 0.2);

  }
}


@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 100;
  }
}

@keyframes slide-right {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0%);
  }
}

@keyframes slide-left {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0%);
  }
}

@keyframes slide-top {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0%);
  }
}

@keyframes slide-bottom {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0%);
  }
}

.fade-enter-active {
  animation: fade 0.2s linear;
}
.fade-leave-active {
  animation: fade 0.2s linear reverse;
}

.slide-right-enter-active {
  animation: slide-right 0.5s ease;
}
.slide-right-leave-active {
  animation: slide-right 0.2s ease reverse;
}

.slide-left-enter-active {
  animation: slide-left 0.5s ease;
}
.slide-left-leave-active {
  animation: slide-left 0.2s ease reverse;
}
.slide-bottom-enter-active {
  animation: slide-bottom 0.5s ease;
}
.slide-bottom-leave-active {
  animation: slide-bottom 0.2s ease reverse;
}
.slide-top-enter-active {
  animation: slide-top 0.5s ease;
}
.slide-top-leave-active {
  animation: slide-top 0.2s ease reverse;
}



</style>