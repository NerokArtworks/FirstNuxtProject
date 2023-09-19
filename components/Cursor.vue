<script setup>
onMounted(() => {
  const customCursor = document.querySelector(".cursor");

  document.addEventListener("mousemove", (e) => {
    customCursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px) scale(1.5)`;
  });

  // Al hacer hover sobre elementos con clase "target"
  //   const targetElements = document.querySelectorAll(".will-animate-image");
  //   targetElements.forEach((element) => {
  //     element.addEventListener("mouseenter", (e) => {
  //       customCursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px) scale(1)`;
  //       customCursor.style.opacity = 1;
  //       console.log("hasiendo el hover");
  //     });

  //     element.addEventListener("mouseleave", (e) => {
  //       customCursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px) scale(1.5)`;
  //       customCursor.style.opacity = 0;
  //     });
  //   });
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
