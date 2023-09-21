<script setup>
import Lenis from "@studio-freight/lenis";

onMounted(() => {
  const lenis = new Lenis({
    lerp: 0.05,
    duration: 2,
    easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  });

  lenis.on("scroll", (e) => {
    // console.log(e)
  });

  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }

  requestAnimationFrame(raf);
});
</script>

<template>
  <Cursor></Cursor>
  <BaseHeader></BaseHeader>
  <main class="min-h-screen relative">
    <slot></slot>
  </main>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
