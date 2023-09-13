<script setup>
import { ref } from "vue";

const posts = ref([]);

const response = await fetch("https://jsonplaceholder.typicode.com/posts");
posts.value = await response.json();
</script>

<template>
  <div class="main-hero w-full h-screen relative overflow-hidden text-white">
    <div class="outer">
      <div class="background-image absolute w-full h-full left-0 top-0">
        <div class="media">
          <video
            autoplay=""
            playsinline=""
            loop=""
            muted=""
            class="will-animate-image h-full w-full left-0 top-0 object-cover absolute"
            style="opacity: 1"
          >
            <source
              type="video/mp4"
              src="https://server.ac3-studio.com/uploads/Showreel_AC_3_V4_mp4_edit_52746e5e16.mp4"
            />
          </video>
        </div>
      </div>
      <div class="content flex items-end py-20 min-h-screen">
        <div class="px-layout w-full px-5">
          <div class="grid grid-cols-2 gap-x-mb lg:gap-x-lg lg:grid-cols-12 content-between lg:items-end min-h-full">
            <div class="col-start-1 col-end-3 lg:col-start-1 lg:col-end-9">
              <div class="content__title">
                <div class="text-9xl lg:text-big-title pb-16" style="line-height: 8rem;">
                  <h1 class="will-animate-reveal animate-reveal">
                    <div class="split-line" style="display: block; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Creative</div>
                    </div>
                    <div class="split-line" style="display: block; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Technologists.</div>
                    </div>
                  </h1>
                </div>
                <div class="play-reel__wrapper">
                  <button class="button--light play-real__button text-5xl border-4 py-2 px-6 pb-4 hover:bg-white hover:text-black transition duration-300 ease-in-out rounded-full will-animate-reveal animate-reveal" style="translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;">
                    <span>Play reel</span>
                  </button>
                </div>
              </div>
            </div>
            <div class="col-start-1 col-end-3 lg:col-start-10 lg:col-end-13">
              <div class="content__paragraph">
                <p class="text-2xl will-animate-reveal animate-reveal" style="">
                  <div class="split-line" style="display: block; text-align: start; position: relative;">
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">AC3</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">is</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">a</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">multidisciplinary</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">creative</div>
                  </div>
                  <div class="split-line" style="display: block; text-align: start; position: relative;">
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">technology</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">studio</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">based</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">in</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Paris,</div>
                  </div>
                  <div class="split-line" style="display: block; text-align: start; position: relative;">
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Hong-Kong</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">and</div>
                    <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Saigon.</div>
                  </div>
                </p>
              </div>
              <div class="scroll-to__wrapper">
                <div class="text-small-paragraph">
                  <button class="scroll-to will-animate-reveal animate-reveal" style="">
                    <span style="">
                      <div class="split-line" style="display: block; text-align: center; position: relative;">
                        <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Scroll</div>
                        </div> 
                        <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">to</div>
                        </div> 
                        <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">discover</div>
                        </div>
                      </div>
                    </span>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
