<template>
  <div class="container mx-auto bg-red-500">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laborum dignissimos numquam ipsum, possimus aliquid quod quas soluta corrupti similique, consequuntur atque est ratione earum sequi odit minima eligendi maxime unde!
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  }
})
</script>

<style>
html,body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>