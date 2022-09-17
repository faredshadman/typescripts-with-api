<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-5">
    <PostElement v-for="post in posts" :key="post.id" :post="post" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";
import { Product } from "../types";
import PostElement from "./PostElement.vue";
export default defineComponent({
  name: "PostContainer",
  props: {
    posts: Array as PropType<Product[]>,
  },
  components: { PostElement },
});
</script>
