<script setup lang="ts">
  import { useRouter } from "vue-router";

  import generatedRoutes from "virtual:generated-pages";
  const router = useRouter();

  const leftDrawerOpen = ref<boolean>(true);
  const toolbarShow = ref<boolean>(true);
  const hiddenPages = ref<string[]>(["répa", "körte"]);

  function toggleLeftDrawer(): void {
    leftDrawerOpen.value = !leftDrawerOpen.value;
  }

  onMounted(() => {
    // show left drawer on start
    leftDrawerOpen.value = false;
    // show toolbar on start
    toolbarShow.value = true;
  });
</script>

<template>
  <q-layout view="hHh Lpr fFf">
    <q-page-container id="container">
      <router-view v-slot="{ Component }">
        <transition mode="out-in" name="slide-fade">
          <component :is="Component" />
        </transition>
      </router-view>
    </q-page-container>
  </q-layout>
</template>

<style lang="scss">
  .slide-fade-enter {
    transform: translateX(10px);
    opacity: 0;
  }

  .slide-fade-enter-active,
  .slide-fade-leave-active {
    transition: all 0.2s ease;
  }

  .slide-fade-leave-to {
    transform: translateX(-10px);
    opacity: 0;
  }

  #title {
    font-size: 10px;
    @media (min-width: 400px) {
      font-size: calc(10px + 0.5vw);
    }
    @media (min-width: 800px) {
      font-size: calc(14px + 0.5vw);
    }
    @media (min-width: 1200px) {
      font-size: calc(18px + 0.5vw);
    }
  }
</style>
