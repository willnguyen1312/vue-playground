<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <button @click="loadMe">Load me</button>
  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
</template>

<script lang="ts">
import { defineComponent, defineAsyncComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  components: {
    HelloWorld: defineAsyncComponent({
      loader: () => import("./components/HelloWorld.vue"),
    }),
  },
  setup() {
    const showHello = ref(false);
    const loadMe = () => {
      const resize = new ResizeObserver(() => {});
      showHello.value = true;
    };
    return { loadMe, showHello };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
