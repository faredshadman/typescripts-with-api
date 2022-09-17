<template>
  <NavBar :toggleMenu="toggleMenu" :isMobile="isMobile" />
  <router-view class="py-16" />
  <FooterEl />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import NavBar from "./components/NavBar.vue";
import FooterEl from "./components/FooterEl.vue";
export default defineComponent({
  name: "App",
  components: {
    NavBar,
    FooterEl,
  },
  data() {
    return {
      isMobile: false,
    };
  },
  methods: {
    toggleMenu(): void {
      this.isMobile = !this.isMobile;
    },
  },
});
</script>
