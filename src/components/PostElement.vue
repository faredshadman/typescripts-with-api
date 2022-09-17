<template>
  <div class="bg-white pb-2 rounded shadow-xl shadow-slate-500 flex flex-col">
    <div class="w-full relative">
      <h2 class="px-2 absolute top-0 right-5 text-blue-700">
        {{ post.title }}
      </h2>
      <img
        class="w-full h-40 shadow-lg"
        :key="post.description"
        :src="post.thumbnail"
        :alt="post.description"
      />
    </div>
    <p class="font-semibold p-2">{{ post.description }}</p>

    <button
      class="bg-blue-400 px-2 py-0.5 text-white self-end mr-2 mt-auto rounded text-lg"
    >
      <router-link :to="'/' + post.id" class="block"> See more </router-link>
    </button>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";
import { Product } from "../types";
export default defineComponent({
  name: "PostElement",
  props: {
    post: {
      type: Object as PropType<Product>,
      required: true,
    },
  },
});
</script>
