<script lang="ts" setup>
import Accordion from "~/components/shared/accordion.vue";

type MenuItem = {
  id: number;
  text: string;
  children: MenuItem[];
  [key:string]: any
}
type Props = {
  items: MenuItem[]
}

defineProps<Props>()
</script>
<template>
  <ul class="menu-list">
    <li class="menu-list-item" v-for="menu of items" :key="menu.id">
      <template v-if="menu.children && menu.children.length">
        <accordion :text="menu.text">
          <template #content>
            <tree-list :items="menu.children"/>
          </template>
        </accordion>
      </template>
      <template v-else>
        <span>{{menu.text}}</span>
      </template>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
.menu-list {
  margin: 0;
  padding: 0;
  &-item {
    padding: 10px;
    list-style: none;
    color: white;
  }
}
</style>