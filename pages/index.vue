<script setup>
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);


const main = ref();
const work = ref();
let cursorAnimating = false; // Variable de estado para controlar si el cursor está animando
let currentEvent = null; // Variable para hacer un seguimiento del evento actual

let ctx;
let ctxWork;

onMounted(() => {
  const cursor = document.querySelector(".cursor");
  const cursorText = document.querySelector(".cursor-text");
  const targetElements = document.querySelectorAll(".will-animate-image");
  const crafts = document.querySelector(".crafts");
  const pageInner = document.querySelector(".page__inner");

  ctx = gsap.context((self) => {
    const lines = self.selector('.scroll');
    lines.forEach((line) => {
      gsap.to(line, {
        y: 200,
        scrollTrigger: {
          trigger: line,
          start: 'top center',
          end: 'top -100%',
          scrub: true,
        },
      });
    });
    
    if (cursor != undefined) {
      targetElements.forEach((element) => {
        // MOUSEOVER
        element.addEventListener("mouseover", (e) => {
          if (!cursorAnimating || currentEvent !== "mouseover") {
            if (currentEvent !== "mouseover") {
              console.log("Repitiendo mousein");
              currentEvent = "mouseover"; // Actualiza el evento actual
              cursorAnimating = true; // Inicia la animación del cursor
              gsap.to(cursor, {
                x: e.clientX,
                y: e.clientY,
                scale: 1,
                opacity: 1,
                ease: "power2.out",
                onComplete: () => {
                  cursorAnimating = false; // Finaliza la animación del cursor
                }
              });
              gsap.to(cursorText, {
                opacity: 1,
                y: '0%',
                rotate: 0,
                ease: "power2.out"
              });
            } else {
              currentEvent = "mouseover"; // Actualiza el evento actual
              cursorAnimating = true; // Inicia la animación del cursor

              // Detén cualquier animación en curso en el elemento del cursor
              gsap.killTweensOf(cursor);

              gsap.fromTo(cursor, {
                x: e.clientX,
                y: e.clientY,
                scale: 1.5,
                opacity: 0,
              }, {
                x: e.clientX,
                y: e.clientY,
                scale: 1,
                opacity: 1,
                ease: "power2.out",
                onComplete: () => {
                  cursorAnimating = false; // Finaliza la animación del cursor
                },
              });

              gsap.fromTo(cursorText, {
                y: '100%',
                rotate: 10,
                opacity: 0
              }, {
                y: '0%',
                rotate: 0,
                opacity: 1,
                ease: "power2.out"
              });
            }
          }
        });

        // MOUSELEAVE
        element.addEventListener("mouseleave", (e) => {
          if (!cursorAnimating || currentEvent !== "mouseleave") {
            currentEvent = "mouseleave"; // Actualiza el evento actual
            cursorAnimating = true; // Inicia la animación del cursor

            // Detén cualquier animación en curso en el elemento del cursor
            gsap.killTweensOf(cursor);

            gsap.fromTo(
              cursor,
              {
                x: e.clientX,
                y: e.clientY,
                scale: 1.005,
                opacity: 1,
              },
              {
                scale: 0.5,
                opacity: 0,
                ease: "circ.in",
                duration: .6,
                onComplete: () => {
                  cursorAnimating = false; // Finaliza la animación del cursor
                  if (currentEvent == "mouseleave") {
                    gsap.to(cursor, {
                    x: e.clientX,
                    y: e.clientY,
                    scale: 1.5,
                    opacity: 0,
                    duration: 0
                  })
                  }
                },
              }
            );

            gsap.fromTo(cursorText, {
                y: '0%',
                rotate: 0,
                opacity: 1
              }, {
                y: '100%',
                rotate: 10,
                opacity: 0,
                ease: "circ.in",
                duration: .5
              });
          }
        });

        // WORK LIST IMAGES
        gsap.fromTo(element, {
          opacity: 0,
          scale: 1.5
        }, {
          opacity: 1,
          scale: 1,
          ease: 'power2.out',
          duration: 1,
          scrollTrigger: {
            trigger: element,
            start: 'top 80%',
            end: 'bottom bottom',
            toggleActions: "play resume resume reset"
          },
        });
      });

      document.addEventListener("mousemove", (e) => {
        gsap.to(cursor, { x: e.clientX, y: e.clientY, ease: "power3.out" });
      });
    }

  }, main.value); // <- Scope!

  ctxWork = gsap.context((self) => {
    // const workListSection = self.selector('.works-featured-list.bg-white');
    // gsap.to(workListSection, {
    //   yPercent: -20,
    //   scrollTrigger: {
    //     trigger: workListSection,
    //     start: 'top bottom',
    //     end: 'bottom top',
    //     scrub: true
    //   },
    // })

    const lines = self.selector('.split-line > div');
    lines.forEach((line) => {
      gsap.from(line, {
        yPercent: 100,
        rotation: 3,
        opacity: 0,
        scrollTrigger: {
          trigger: line,
          start: 'top bottom',
          end: 'top 50%',
          ease: 'Power4.easeOut',
          scrub: true
        },
      });
    });

    // CRAFTS SECTION BG
    gsap.fromTo(pageInner, {
      background: 'rgba(255,255,255,1)'
    }, {
      background: 'rgba(0,0,0,1)',
      ease: 'power2.out',
      scrollTrigger: {
        trigger: crafts,
        start: 'top 50%',
        end: 'top -30%',
        scrub: true
      },
    });
  }, work.value); // <- Scope!

 
  
});

onUnmounted(() => {
  ctx.revert(); // <- Easy Cleanup!
  ctxWork.revert(); // <- Easy Cleanup!
});

</script>

<template>
  <div class="page__inner bg-white">
    <section class="main-hero w-full h-screen relative overflow-hidden text-white">
      <div class="outer">
        <div class="background-image absolute w-full h-full left-0 top-0">
          <div class="media">
            <video
              autoplay=""
              playsinline=""
              loop=""
              muted=""
              class="h-full w-full left-0 top-0 object-cover absolute"
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
          <div class="px-layout w-full px-5" ref="main">
            <div class="grid grid-cols-2 gap-x-mb lg:gap-x-lg lg:grid-cols-12 content-between lg:items-end min-h-full scroll">
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
                  <p class="text-2xl will-animate-reveal animate-reveal">
                    <div class="split-line gap-1" style="display: flex; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">AC3</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">is</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">a</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">multidisciplinary</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">creative</div>
                    </div>
                    <div class="split-line gap-1" style="display: flex; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">technology</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">studio</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">based</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">in</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Paris,</div>
                    </div>
                    <div class="split-line gap-1" style="display: flex; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Hong-Kong</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">and</div>
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Saigon.</div>
                    </div>
                  </p>
                </div>
                <div class="scroll-to__wrapper">
                  <div class="text-small-paragraph">
                    <button class="scroll-to will-animate-reveal animate-reveal" >
                      <span >
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
    </section>

    <!-- WORK LIST SECTION -->
    <!-- Poner bg-white al section para activar gsap bg animation -->
    <section class="min-h-screen relative works-featured-list" ref="work"> 
      <div class="works-featured-list">
          <div class="works__outer">
              <div class="px-layout px-5">
                  <h2 class="text-9xl">
                    <div class="split-line" style="display: block; text-align: start; position: relative;">
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">
                        Our
                      </div> 
                      <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">
                        Work
                      </div>
                    </div>
                  </h2>

                  <div class="works__list mt-32">
                    <div class="studio__shot-presentation">
                      <p class="will-animate-reveal animate-reveal" data-v-1bee7bc8="" style="">
                        <div class="split-line" style="display: block; text-align: start; position: relative;">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">We</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">believe</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">that</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">creativity</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">knows</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">no</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">bounds.</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">Our</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">collaborative</div> 
                        </div>
                        <div class="split-line" style="display: block; text-align: start; position: relative;">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">approach,</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">technical</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">abilities,</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">and</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">artistic</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">vision</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">are</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">dedicated</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">to</div> 
                        </div>
                        <div class="split-line" style="display: block; text-align: start; position: relative;">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">elevating</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">every</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">project</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">we</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">touch.</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">We’re</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">here</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">to</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">push</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">the</div> 
                        </div>
                        <div class="split-line" style="display: block; text-align: start; position: relative;">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">boundaries</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">of</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">what’s</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">possible</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">in</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">the</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">world</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">of</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">art,</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">design,</div> 
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">and</div> 
                        </div>
                        <div class="split-line" style="display: block; text-align: start; position: relative;">
                          <div style="position: relative; display: inline-block; translate: none; rotate: none; scale: none; transform: translate(0px, 0px); opacity: 1;" class="split-word">technology.</div>
                        </div>
                      </p>
                    </div>
                    <div class="works__list__item">
                      <div class="work__thumbnail">
                        <div class="work__outer">
                          <a href="" class="animate-media-hover">
                            <figure class="work__inner">
                              <div class="work__image overflow-hidden">
                                <div class="work__image__inner absolute inset-0">
                                  <div class="media h-full">
                                    <picture class="flex h-full">
                                      <img class="will-animate-image object-cover" draggable="false" data-nuxt-pic="" src="/img/01.jpg" style="opacity: 1;">
                                    </picture>
                                  </div>
                                </div>
                              </div>
                            </figure>
                          </a>
                        </div>
                      </div>
                    </div>
                    <div class="works__list__item">
                      <div class="work__thumbnail">
                        <div class="work__outer">
                          <a href="" class="animate-media-hover">
                            <figure class="work__inner">
                              <div class="work__image overflow-hidden">
                                <div class="work__image__inner absolute inset-0">
                                  <div class="media h-full">
                                    <picture class="flex h-full">
                                      <img class="will-animate-image object-cover" draggable="false" data-nuxt-pic="" src="/img/02.jpg" style="opacity: 1;">
                                    </picture>
                                  </div>
                                </div>
                              </div>
                            </figure>
                          </a>
                        </div>
                      </div>
                    </div>
                    <div class="works__list__item">
                      <div class="work__thumbnail">
                        <div class="work__outer">
                          <a href="" class="animate-media-hover">
                            <figure class="work__inner">
                              <div class="work__image overflow-hidden">
                                <div class="work__image__inner absolute inset-0">
                                  <div class="media h-full">
                                    <picture class="flex h-full">
                                      <img class="will-animate-image object-cover" draggable="false" data-nuxt-pic="" src="/img/03.jpg" style="opacity: 1;">
                                    </picture>
                                  </div>
                                </div>
                              </div>
                            </figure>
                          </a>
                        </div>
                      </div>
                    </div>
                    <div class="works__list__item">
                      <div class="work__thumbnail">
                        <div class="work__outer">
                          <a href="" class="animate-media-hover">
                            <figure class="work__inner">
                              <div class="work__image overflow-hidden">
                                <div class="work__image__inner absolute inset-0">
                                  <div class="media h-full">
                                    <picture class="flex h-full">
                                      <img class="will-animate-image object-cover" draggable="false" data-nuxt-pic="" src="/img/05.jpg" style="opacity: 1;"></picture>
                                  </div>
                                </div>
                              </div>
                            </figure>
                          </a>
                        </div>
                      </div>
                    </div>
                    <div class="works__list__item">
                      <div class="work__thumbnail">
                        <div class="work__outer">
                          <a href="" class="animate-media-hover">
                            <figure class="work__inner">
                              <div class="work__image overflow-hidden">
                                <div class="work__image__inner absolute inset-0">
                                  <div class="media h-full">
                                    <picture class="flex h-full">
                                      <img class="will-animate-image object-cover target" draggable="false" data-nuxt-pic="" src="/img/04.jpg" style="opacity: 1;">
                                    </picture>
                                  </div>
                                </div>
                              </div>
                            </figure>
                          </a>
                        </div>
                      </div>
                    </div>
                  </div>
              </div>
          </div>
      </div>
    </section>

    <!-- BLACK BG SECTION -->
    <section class="w-full h-screen relative mix-blend-difference text-white crafts">
      <div class="crafts__outer">
        <div class="px-layout px-5">
          <div class="crafts__inner">
          
          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<style>
.works-featured-list {
    /* padding: 72rem 0 */
}

@media (min-width: 1024px) {
    .works-featured-list {
        padding:2rem 0
    }
}

.works-featured-list .works__inner {
    position: relative
}

.works-featured-list .works__list {
    grid-row-gap: 36rem;
    -moz-column-gap: 18rem;
    column-gap: 18rem;
    display: grid;
    grid-template-columns: repeat(2,minmax(0,1fr));
    /* margin-top: 37rem */
}

@media (min-width: 1024px) {
    .works-featured-list .works__list {
        grid-row-gap:10rem;
        -moz-column-gap: 5rem;
        column-gap: 5rem;
        grid-template-columns: repeat(12,minmax(0,1fr));
        margin-top: 8rem;
    }
}

.works-featured-list .studio__shot-presentation,.works-featured-list .works__list__item {
    grid-column: auto/span 2;
    grid-row: auto/auto
}

@media (min-width: 1024px) {
    .works-featured-list .studio__shot-presentation {
        grid-column:8/span 4;
        grid-row: auto/auto
    }

    .works-featured-list .works__list__item:nth-of-type(5n+2) {
        grid-column: 1/span 6;
        grid-row: 1/span 2
    }
}

.works-featured-list .works__list__item:nth-of-type(5n+2) .work__image {
    overflow: hidden;
    position: relative
}

.works-featured-list .works__list__item:nth-of-type(5n+2) .work__image:before {
    content: "";
    display: block;
    padding-top: 100%;
    width: 100%
}

.works-featured-list .works__list__item:nth-of-type(5n+2) .work__image :deep(img) {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%
}

@media (min-width: 1024px) {
    .works-featured-list .works__list__item:nth-of-type(5n+3) {
        grid-column:8/span 4;
        grid-row: auto/auto
    }
}

.works-featured-list .works__list__item:nth-of-type(5n+3) .work__image {
    overflow: hidden;
    position: relative
}

.works-featured-list .works__list__item:nth-of-type(5n+3) .work__image:before {
    content: "";
    display: block;
    padding-top: 133.3333333333%;
    width: 100%
}

.works-featured-list .works__list__item:nth-of-type(5n+3) .work__image :deep(img) {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%
}

@media (min-width: 1024px) {
    .works-featured-list .works__list__item:nth-of-type(5n+4) {
        grid-column:2/span 8;
        grid-row: auto/auto
    }
}

.works-featured-list .works__list__item:nth-of-type(5n+4) .work__image {
    overflow: hidden;
    position: relative
}

.works-featured-list .works__list__item:nth-of-type(5n+4) .work__image:before {
    content: "";
    display: block;
    padding-top: 75%;
    width: 100%
}

.works-featured-list .works__list__item:nth-of-type(5n+4) .work__image :deep(img) {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%
}

@media (min-width: 1024px) {
    .works-featured-list .works__list__item:nth-of-type(5n+5) {
        grid-column:2/span 4;
        grid-row: auto/auto
    }
}

.works-featured-list .works__list__item:nth-of-type(5n+5) .work__image {
    overflow: hidden;
    position: relative
}

.works-featured-list .works__list__item:nth-of-type(5n+5) .work__image:before {
    content: "";
    display: block;
    padding-top: 133.3333333333%;
    width: 100%
}

.works-featured-list .works__list__item:nth-of-type(5n+5) .work__image :deep(img) {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%
}

@media (min-width: 1024px) {
    .works-featured-list .works__list__item:nth-of-type(5n+6) {
        grid-column:9/span 4;
        grid-row: auto/auto
    }
}

.works-featured-list .works__list__item:nth-of-type(5n+6) .work__image {
    overflow: hidden;
    position: relative
}

.works-featured-list .works__list__item:nth-of-type(5n+6) .work__image:before {
    content: "";
    display: block;
    padding-top: 75%;
    width: 100%
}

.works-featured-list .works__list__item:nth-of-type(5n+6) .work__image :deep(img) {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%
}

.works-featured-list .browse-all {
    display: flex;
    justify-content: center;
    margin-top: 48rem
}

@media (min-width: 1024px) {
    .works-featured-list .browse-all {
        bottom:0;
        margin-top: 0;
        position: absolute;
        right: 0
    }
}

.works-featured-list .browse-all .browse-all__button {
    align-items: center;
    border: 2px solid #1e1f22;
    border-radius: 999rem;
    display: flex;
    justify-content: center;
    transition: background .2s linear
}

@media (hover: hover) and (pointer:fine) {
    .works-featured-list .browse-all .browse-all__button:hover {
        background:#000
    }

    .works-featured-list .browse-all .browse-all__button:hover span {
        color: #fff
    }
}

.works-featured-list .browse-all .browse-all__button span {
    padding: 8rem 32rem;
    transition: color .2s linear
}

.split-line {
  overflow: hidden;
}

.split-word {
  margin-right: 4px;
}
</style>