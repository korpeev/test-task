<script lang="ts" setup>
type Props = {
  show?: boolean
  text?: string
}

type AccordionEmits = {
  (event: "update:show", payload: boolean): void
}

const props = defineProps<Props>()

const emit = defineEmits<AccordionEmits>()
const isShow = ref(props.show)
const onChangeShow = () => {
  isShow.value = !isShow.value
  emit('update:show', !isShow.value)

}

</script>
<template>
  <div class="accordion">
    <div @click="onChangeShow" class="accordion-activator">
      <slot name="activator" :props="{isShow}">
        <div class="accordion-activator-item">
          <span>{{text}}</span>
          <img class="accordion-icon" :class="{'active': isShow}" src="~/assets/icons/chevron-down.svg" alt="chevron down">
        </div>
      </slot>
    </div>
    <transition name="slide-down">
      <div v-if="isShow">
        <slot name="content"/>
      </div>
    </transition>
  </div>
</template>

<style lang="scss" scoped>
.accordion {
  position: relative;
  &-activator {
    border-radius: 12px;
    padding: 10px 0;
    position: relative;
    z-index: 10;
    cursor: pointer;
    margin-bottom: 10px;
    &-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  }
  &-icon {
    width: 20px;
    height: 20px;
    transform: rotate(-90deg);
    transition: transform .3s ease;
    &.active {
      transform: rotate(0deg);
    }
  }
  &-content {
    position: relative;
    padding: 10px 0;
    border-radius: 12px;
    margin-bottom: 20px;
    &.active {
      animation: slideDown .3s ease forwards;
    }
  }
}

@keyframes slide-down {
  from {
    opacity: 0;
    transform: translateY(-100%);
  }
  to {
    opacity: 100;
    transform: translateY(0%);
  }
}

.slide-down-enter-active {
  animation: slide-down 0.2s linear;
}
.slide-down-leave-active {
  animation: slide-down 0.2s linear reverse;
}

</style>