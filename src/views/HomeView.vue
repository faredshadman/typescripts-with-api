<template>
  <section class="dark:bg-gray-900 bg-slate-300 px-10 py-2">
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
    <div v-if="!loading" class="flex flex-col gap-3">
      <PostContainer :posts="posts" />
      <div class="self-end flex items-center gap-3">
        <select class="px-3 py-1" id="limit" v-model="limit">
          <option :value="4">4</option>
          <option :value="8">8</option>
          <option :value="12">12</option>
        </select>
        <select class="px-3 py-1" id="skip" v-model="skip">
          <option v-for="page in pages" :key="page" :value="page - 1">
            {{ page }}
          </option>
        </select>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { Post, Product } from "../types";
import { defineComponent } from "vue";
import PostContainer from "@/components/PostContainer.vue";

export default defineComponent({
  name: "HomeView",
  async mounted() {
    await this.getPosts();
  },
  computed: {
    pagination(): number {
      return this.skip * this.limit;
    },
    pages(): number {
      return Math.ceil(100 / Number(this.limit));
    },
  },
  data() {
    return {
      posts: [] as Product[],
      limit: 8 as number,
      skip: 0 as number,
      loading: false as boolean,
    };
  },
  watch: {
    limit() {
      this.skip = 0;
      this.getPosts();
    },
    skip() {
      this.getPosts();
    },
  },
  methods: {
    async getPosts(): Promise<void> {
      this.loading = true;

      await fetch(
        `https://dummyjson.com/products?limit=${this.limit}&skip=${this.pagination}`
      )
        .then((res: Response) => res.json())
        .then((data: Post) => {
          this.posts = data.products as Product[];
          console.log(this.posts);
        })
        .catch((err) => {
          console.log(err);
        })
        .finally(() => {
          this.loading = false;
        });
    },
  },
  components: { PostContainer },
});
</script>
