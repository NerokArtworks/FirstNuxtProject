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
      <div class="inner">
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
  height: 8rem;
  justify-content: center;
  left: 0;
  pointer-events: none;
  position: fixed;
  top: 0;
  width: 8rem;
  z-index: 999;
}

@media (hover: hover) and (pointer: fine) {
  .cursor {
    display: flex;
  }
}

.inner {
  overflow: hidden;
}

.cursor-text {
  color: #fff;
  /* font-size: 4rem; */
  line-height: 8rem;
  text-transform: uppercase;
}

.cursor-text span {
  display: block;
}
</style>
