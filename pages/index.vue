<template>
  <div>
    <h1>Swiper - Vue</h1>
    <Swiper
      ref="swiper"
      class="carousel-style"
      :slides-per-view="1"
      loop
      autoplay
      @swiper="onSwiper"
      @slideChange="onSlideChange"
    >
      <SwiperSlide
        v-for="(el, i) in [0, 1, 2, 3, 4, 5, 6, 7]"
        :key="i"
        class="video-card"
        @mouseenter="playVideo(i)"
        @mouseleave="pauseVideo(i)"
      >
        <!-- <div class="video-container" :class="{ active: currentIndex == i }"> -->
        <div class="video-container">
          <video
            :id="`carrouselVideo${i}`"
            loop
            muted
            playsinline
            :controls="false"
          >
            <source src="https://cdn.sandbox.game/home/Hero-Video-low.mp4" />
          </video>
          <!-- <nuxt-img
            class="partner-logo"
            src="/img/00_General/testpartnerlogo.png"
            alt="Partner Logo"
            height="64"
          /> -->
        </div>
      </SwiperSlide>
    </Swiper>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  setup() {
    const i = 1;
    // const swiper = ref(null);
    // const swiperSlide = ref(null);
    // //REF:: https://swiperjs.com/vue#useswiper
    const swiper = useSwiper();
    // //REF:: https://swiperjs.com/vue#useswiperslide
    const swiperSlide = useSwiperSlide();
    const onSwiper = (swiper) => {
      console.log("onSwiper:: ", { swiper });
    };
    const onSlideChange = (ev) => {
      console.log("onSlideChange:: ", { ev });
      console.log("activeIndex:: ", swiper.value.activeIndex);

      console.log("swiperSlide:: ", { swiperSlide: swiperSlide.value });
    };

    function playVideo(index) {
      const video = document.getElementById(`carrouselVideo${index}`);
      video?.play();
    }
    function pauseVideo(index) {
      const video = document.getElementById(`carrouselVideo${index}`);
      video?.pause();
      video.currentTime = 0;
    }
    return {
      i,
      swiper,
      swiperSlide,
      onSwiper,
      onSlideChange,
      playVideo,
      pauseVideo,
    };
  },
};
</script>


<style lang="scss" scoped>
.container {
  position: relative;
}
.carousel-style {
  max-width: 1440px;
  :deep(.ssr-carousel-slide) {
    width: 302px;
  }
  .video-card {
    height: 220px;
    .video-container {
      width: 302px;
      height: 160px;
      overflow: hidden;
      position: relative;
      transition: height 0.5s;
      .partner-logo {
        position: absolute;
        left: 50%;
        top: 50%;
        -webkit-transform: translate(-50%, -50%);
        -moz-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);
        transition: transform 0.5s;
      }
      &:hover {
        height: 220px;
        .partner-logo {
          transform: translate(-50%, 80%) scale(0.75);
        }
      }
    }
    video {
      width: 302px;
      height: 220px;
      object-fit: cover;
    }
  }
}

.full-screen-video {
  height: calc(100dvh - var(--navbar-height-redesign));
  width: 100%;
  object-fit: cover;
  position: sticky;
  top: 0;
  z-index: 0;
}
.grid {
  position: sticky;
  top: 0;
  display: grid;
  grid: [a] 1fr / [b] 1fr;
}
.sticky-background {
  grid-area: a / b;
  position: sticky;
  top: 0;
  z-index: 2;
  height: calc(100dvh - var(--navbar-height-redesign));
  background: radial-gradient(
      200% 100% at 100% 0%,
      #0d1015 31.96%,
      rgba(1, 10, 48, 0) 64.77%
    ),
    radial-gradient(
      200% 100% at 0% 100%,
      #0d1015 29.86%,
      rgba(1, 10, 48, 0) 67.84%
    ),
    #020b31;
}
.content {
  grid-area: a / b;
  z-index: 4;
  position: sticky;
  height: calc(100dvh - var(--navbar-height-redesign));
}
</style>
