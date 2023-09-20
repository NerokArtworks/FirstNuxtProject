<script setup>
import { gsap } from "gsap";

// const cursor = ref();
// let ctx;

onMounted(() => {});

// Limpia el contexto cuando el componente se desmonta
onUnmounted(() => {
  ctx.revert();
});
</script>

<template>
  <div class="cursor">
    <div class="outer">
      <div class="inner overflow-hidden w-full">
        <div class="cursor-text">
          <span>View</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.cursor {
  align-items: center;
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  background: hsla(0, 0%, 42%, 0.5);
  border-radius: 50%;
  display: none;
  height: 9rem;
  justify-content: center;
  left: 0;
  pointer-events: none;
  position: fixed;
  top: 0;
  width: 9rem;
  z-index: 999;
}

@media (hover: hover) and (pointer: fine) {
  .cursor {
    display: flex;
  }
}

.cursor-text {
  color: #fff;
  /* font-size: 4rem; */
  /* line-height: 8rem; */
  text-transform: uppercase;
  transform: translateY(100%);
  transform-origin: top left;
  height: min-content;
}

.cursor-text span {
  display: block;
  font-size: 1.1rem;
}
</style>
