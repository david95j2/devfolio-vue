<template>
  <TitleBar title="게시물 리스트" />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TitleBar from '../components/TitleBar.vue';

export default defineComponent({
  name: 'ArticleListPage',
  components: {
    TitleBar
  }
})
</script>

<style scoped>
  h1 {
    color:red;
  }
</style>