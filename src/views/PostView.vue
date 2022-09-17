<template>
  <section class="px-10 dark:bg-gray-900 bg-slate-300">
    <div
      class="flex justify-center items-center h-screen w-full"
      v-if="loading"
    >
      <div
        class="spinner-border animate-spin inline-block w-8 h-8 border-4 rounded-full"
        role="status"
      >
        <span class="opacity-0">Loading...</span>
      </div>
    </div>
    <div v-if="!loading">
      <router-link to="/">
        <button class="bg-blue-400 px-3 py-1 text-white rounded text-xl">
          Back to Home
        </button>
      </router-link>
      <h1 class="font-medium text-2xl dark:text-white">
        {{ post.title }}
      </h1>
      <p class="dark:text-white">{{ post.description }}</p>
      <div
        class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 place-items-center gap-10"
      >
        <img
          class="aspect-square"
          v-for="image in post.images"
          :key="image"
          :src="image"
          :alt="post.title"
        />
      </div>
    </div>
  </section>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import { Product } from "@/types";
export default defineComponent({
  name: "SinglePost",
  data() {
    return {
      post: {} as Product,
      loading: false as boolean,
    };
  },

  mounted() {
    let id = Number(this.$route.params.id);
    this.getData(id);
  },
  methods: {
    async getData(id: number): Promise<void> {
      this.loading = true;
      await fetch(`https://dummyjson.com/products/${id}`)
        .then((res: Response) => res.json())
        .then((data: Product) => {
          this.post = data;
        })
        .catch((err) => console.log(err))
        .finally(() => {
          this.loading = false;
        });
    },
  },
});
</script>
