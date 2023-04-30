<template>
  <div data-scroll-container class="wrapper">
    <Navbar />
    <div class="hero-wrapper">
      <div class="container-title">
        <div>
          <h1>
            Lucas Huerta
          </h1>
          <p>
            FullStack developper
          </p>
        </div>
      </div>
      <div class="container-star">
        <img ref="imgStar" src="./assets/star.png" alt="star">
      </div>
      <div class="container-svg">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M14.8382 9.13358L12.2744 0L9.70836 9.13358L0 12L9.70836 14.5087L12.2744 24L14.6552 14.5087L24 12L14.8382 9.13358Z" fill="black"/>
        </svg>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M14.8382 9.13358L12.2744 0L9.70836 9.13358L0 12L9.70836 14.5087L12.2744 24L14.6552 14.5087L24 12L14.8382 9.13358Z" fill="black"/>
        </svg>
      </div>
      <div class="container-ellipse">
        <div class="ellipse">
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue';
import LocomotiveScroll from 'locomotive-scroll';
import { ref, onMounted } from 'vue';

const scrollY = ref(0);
const scroll = new LocomotiveScroll();
let imgStar = ref();

function handleScroll() {
  scrollY.value = window.scrollY;
  imgStar.value.style.transform = `rotate(${scrollY.value/5}deg)`;
  imgStar.value.style.transform = 'all linear';
  imgStar.value.style.position = 'fixed';
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

</script>

<style scoped>
.wrapper{
  width: 100%;
  height: 100vh;
  position: relative;
}

.hero-wrapper{
  width: 100%;
  height: 100%;
}

.hero-wrapper h1{
  font-weight: bold;
  font-size: 110px;
}

.container-title{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center
}

.container-title div{
  width: fit-content;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.container-title div p{
  margin: 0;
}

.container-star img{
  position: absolute;
  top: 20%;
  right: 50%;
  left: 25%;
  bottom: 50%;
  width: 50%;
  height: auto;
  z-index: -1;
}

.container-svg{
  position: absolute;
  bottom: 15%;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.container-svg svg{
  margin: 0 5vw;
}

.container-ellipse{
  position: relative;
  width: 100%;
  height: 100px;
}

.container-ellipse .ellipse{
  position: absolute;
  top: 0;
  background-color: var(--black-color);
  width: 120vw;
  height: 100vw;
  left: 50%;
  border-top-right-radius: 50%;
  border-top-left-radius: 50%;
  -webkit-transform: scale(1) translateX(-50%);
  transform: scale(1) translateX(-50%);
  -webkit-transform-origin: center center;
  transform-origin: center center;
  z-index: 3;
}
</style>
