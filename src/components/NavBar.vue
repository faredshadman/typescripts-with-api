<template>
  <header
    class="z-50 fixed top-0 w-full px-10 py-2 bg-slate-300 dark:bg-gray-900"
  >
    <div class="flex items-center justify-between">
      <h1 class="dark:text-white">LOGO</h1>
      <div class="block md:hidden dark:text-white">
        <button @click="toggleMenu()">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"
            />
          </svg>
        </button>
      </div>
      <nav class="hidden md:block dark:text-white">
        <ul class="flex gap-3">
          <li>Home</li>
          <li>About</li>
          <li>Contact</li>
          <li>FAQ</li>
        </ul>
      </nav>
      <div class="hidden md:block">
        <button class="bg-blue-400 text-white px-3 py-1 rounded">Login</button>
      </div>
    </div>
    <transition name="menu">
      <nav class="mt-5 dark:text-white" v-if="isMobile">
        <ul class="flex flex-col gap-3">
          <li>Home</li>
          <li>About</li>
          <li>Contact</li>
          <li>FAQ</li>
        </ul>
      </nav>
    </transition>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "NavBar",
  props: {
    toggleMenu: {
      type: Function,
      required: true,
    },
    isMobile: {
      type: Boolean,
      required: true,
    },
  },
});
</script>

<style scoped>
.menu-enter-active {
  transition: all 0.5s ease-out;
}

.menu-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}

.menu-enter-from,
.menu-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}
</style>
