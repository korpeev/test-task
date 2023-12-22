<script setup lang="ts">
import {ref} from '#imports'
import Accordion from "~/components/shared/accordion.vue";

const show = ref(false)

</script>
<template>
  <div>
    <h1>Main page</h1>
    <div style="margin-bottom: 20px">
      <nuxt-link class="link"  to="/about-us">about us</nuxt-link>
    </div>

    <accordion v-model:show="show" text="Accordion">
      <template #content>
        <span>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab alias atque blanditiis eius, eligendi esse est magni maiores molestiae officia, omnis praesentium quasi quidem quod ratione repellendus, sit soluta suscipit.</span>
      </template>
    </accordion>
  </div>
</template>
<style lang="scss">
.link {
  cursor: pointer;
  color: white;
}
</style>