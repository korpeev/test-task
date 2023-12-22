<script lang="ts" setup>
type Props = {
  name: string,
  label?: string
  modelValue: boolean
}
type CheckboxEmits = {
  (event: "update:modelValue", payload: boolean): void
}
const props = defineProps<Props>()
const emit = defineEmits<CheckboxEmits>()

const model = computed({
  get() {
    return props.modelValue
  },
  set(newValue: boolean) {
    emit('update:modelValue', newValue)
  }
})

</script>
<template>
  <div class="checkbox">
    <input :value="modelValue" v-model="model" type="checkbox" :id="name"/>
    <img v-if="model" src="~/assets/icons/checkbox.svg" alt="">
    <div v-else class="checkbox-state"/>
    <label :for="name" v-if="label">{{label}}</label>
    <label :for="name" v-else>
      <slot/>
    </label>
  </div>
</template>

<style lang="scss" scoped>
.checkbox {
  display: flex;
  align-items: center;
  gap: 10px;
  img {
    width: 24px;
    height: 24px;
    object-fit: cover;
  }
  &-state {
    width: 18px;
    height: 18px;
    border-radius: 3px;
    border: 1px solid white;
  }
  input {
    display: none;
  }
  label {
    cursor: pointer;
  }
}
</style>