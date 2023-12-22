<script setup lang="ts">
import Checkbox from "~/components/shared/checkbox.vue";
import Drawer from "~/components/shared/drawer.vue";
import MenuList from "~/components/shared/tree-list.vue";
const checked = ref(false)
const drawerShow = ref(false)
const items = [
    {
      id:1, text: "users", children: [{id: 2, text: "John", children: [{id: 4, text: "info", children: []}]}, {id: 2, text: "Mark", children: []}]
    },
  {
    id:1, text: "home", children: []
  },

]
</script>

<template>
  <div class="about">
    <h1>About us page</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facere fuga magnam molestias officiis similique sit? Ad animi culpa est, et, ex exercitationem fugiat ipsum, necessitatibus neque nihil tenetur ullam. Ratione.</p>
    <checkbox v-model="checked" :model-value="checked" name="checkbox-1" label="my checkbox"/>
    <button @click="drawerShow = !drawerShow" style="margin-top: 20px">open menu</button>
    <drawer direction="right" v-model:show="drawerShow" :show="drawerShow">
      <menu-list :items="items"/>
    </drawer>
  </div>
</template>
