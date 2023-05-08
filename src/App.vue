<template>
  <div ref="wrapper" class="wrapper" id="wrapper">
    <Navbar @scrollProject="scrollProject" @scrollContact="scrollContact" data-scroll data-scroll-sticky data-scroll-target="#wrapper" data-scroll-speed="3"/>
    <section class="hero-wrapper">
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
    </section>
    <main class="main">
      <div class="bg">
        <section data-scroll data-scroll-id="project" id="project" class="wrapper-project">
          <Project v-for="project in tabProject" :key="project" :projet="project"/>
        </section>
        <section class="wrapper-competences">
          <div data-scroll data-scroll-direction="horizontal" data-scroll-speed="8" class="high">
            <span v-for="comp in tabHighComp" :key="comp">{{ comp }}</span>
          </div>
          <div data-scroll data-scroll-direction="horizontal" data-scroll-speed="-8" class="bottom">
            <span v-for="comp in tabBottomComp" :key="comp">{{ comp }}</span>
          </div>
        </section>
      </div>
      <section class="wrapper-infos" ref="wrapperInfos" id="wrapperInfos">
        <div class="container-titleInfos">
          <h3 ref="texteInfos">
            About
          </h3>
          <svg width="346" height="201" viewBox="0 0 346 201" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4.75987 178.074C1.24885 170.475 2.01557 160.976 7.06321 149.977C12.1059 138.989 21.2901 126.823 34.0101 114.239C59.4344 89.0857 98.582 62.6522 145.442 41.0003C192.303 19.3483 237.806 6.66907 273.439 3.61074C291.267 2.08063 306.483 2.97139 318.119 6.25302C329.767 9.53787 337.498 15.1108 341.009 22.7096C344.52 30.3084 343.753 39.8076 338.705 50.8064C333.663 61.7945 324.478 73.9597 311.758 86.5442C286.334 111.698 247.187 138.131 200.326 159.783C153.466 181.435 107.963 194.114 72.3296 197.172C54.5019 198.703 39.2851 197.812 27.6492 194.53C16.0017 191.245 8.27089 185.672 4.75987 178.074Z" stroke="#2B58DE" stroke-width="6"/>
          </svg>
        </div>
        <div class="container-infos">
          <div class="row-infos" ref="texteInfos">
            <p>Lucas</p> <p>Huerta</p>
          </div>
          <div class="row-infos" ref="texteInfos">
            <span>21y</span>
            <p>
              Paris
            </p>
          </div>
          <div class="row-infos telNumber" ref="telNumber" @mouseenter="hoverNumberTel" @mouseleave="delHoverNumberTel">
            <span>+</span><span>3</span><span>3</span><span>7</span><span>8</span><span>3</span><span>8</span><span>0</span><span>6</span><span>3</span><span>5</span><span>7</span>
          </div>
          <div class="row-infos" ref="texteInfos">
            <p>Spotify</p> <a href="https://open.spotify.com/playlist/1PA80CpOPlx749kXu7AVsV?si=eee6b25097124095" target="_blank">Playlist</a>
          </div>
        </div>
      </section>
      <section class="footer-section">
        <footer>
          <div class="container-hello">
            <p class="hello">
              Hello
            </p>
            <p class="feel">
              Feel free to send me a message !
            </p>
          </div>
          <div class="bottom-section">
            <a href="mailto:huertalucas13@gmail.com" class="container-contact">Contact me </a>
            <div class="container-bottom">
              <div class="date">
                <p>
                  Local time
                </p>
                <span>{{ formattedDay }}</span>
                <span> {{ formattedDate }}</span>
              </div>
                <p class="footer-name">
                  Lucas huerta 
                </p>
              <div class="rs">
                <span><a href="https://www.linkedin.com/in/lucas-huerta13/" target="_blank">Linkedin</a></span>
                <span><a href="https://github.com/Lucas-Huerta" target="_blank">GitHub</a></span>
                <span><a href="/CV_Huerta_Lucas.pdf" target="_blank">CV</a></span>
              </div>
            </div>
          </div>
        </footer>
      </section>
    </main>
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue';
import Project from './components/Project.vue';
import LocomotiveScroll from 'locomotive-scroll';
import { ref, onMounted } from 'vue';

let scroll = ref();
const wrapper = ref();
let imgStar = ref();

// Ref pour stocker wrapper-infos
let wrapperInfos = ref();
// Ref pour stocker tous les textes
let texteInfos = ref([]);
let telNumber = ref();

let tabProject = ref([
  {
    nom: "Art", 
    tag: "Personal project", 
    image: "/img/Art.png",
    competences: [
      "Vue Js", 
      "Three Js"
    ]
  }, 
  {
    nom: "Abyssal Thoughts", 
    tag: "Personal project", 
    image: "/img/abyssalThought.jpeg",
    competences: [
      "Vue Js", 
      "Pinia"
    ]
  },
  {
    nom: "Calceare", 
    tag: "Student project", 
    image: "/img/HomeCalceare.jpeg", 
    competences: [
      "symfony"
    ]
  },
  {
    nom: "Le défi 24 heures", 
    tag: "Student project", 
    image: "/img/HeroDefi24h.jpeg", 
    competences: [
      "Vue Js",
      "Wordpress Rest API"
    ]
  },
  {
    nom: "Portfolio 2022", 
    tag: "Personnal project", 
    image: "/img/Portfolio2022.jpeg",
    competences: [
      "Three js"
    ]
  }, 
])

let tabHighComp = ref(["Fullstack developper", "Internet child", "Fullstack developper", "Internet child", "Fullstack developper", "Internet child"])
let tabBottomComp = ref(["Vue Js", "Nuxt Js", "Node Js", "CI/CD", "Vue Js", "Nuxt Js", "Node Js", "CI/CD", "Vue Js", "Nuxt Js", "Node Js", "CI/CD"])
let formattedDate = ref();
let formattedDay = ref();

/**
 * Use Locomotive to scroll to #project section
 */
const scrollProject = () =>{
  scroll.value.scrollTo('#project')
}

/**
 * Use Locomotive to scroll to #wrapperInfos section
 */
const scrollContact = () =>(
  scroll.value.scrollTo('#wrapperInfos')
) 

/**
 * Animation au hover numéro téléphone
 */
const hoverNumberTel = () =>{
  wrapperInfos.value.style.background = 'rgba(0, 0, 0, 0.9)';
  wrapperInfos.value.style.opacity = 'rgba(0, 0, 0, 0.9)';
  telNumber.value.style.color = '#FFFFFF';
}

/**
 * Annuler l'animation 
 */
const delHoverNumberTel = () =>{
  wrapperInfos.value.style.background = '';
  telNumber.value.style.color = '#000000';
}

/**
 * Création du scroll Locomotive
 */
const locomotive = async() => {
  scroll.value = await new LocomotiveScroll({
    el: wrapper.value,
    // el: document.querySelector('[data-scroll-container]'),
    // el: document.getElementById('app'),
    smooth: true, 
  });
}

/**
 * Formatage de la date actuelle dans le footer
 */
const haveLocalTime = async() =>{
  const now = new Date();

  // Heure minuets secondes
  const formatter = new Intl.DateTimeFormat('fr', { 
    hour: 'numeric', 
    minute: 'numeric', 
    second: 'numeric' 
  });

  // Mois années, jours
  const formatterDay = new Intl.DateTimeFormat('en', { 
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric', 
  });

  formattedDay.value = formatterDay.format(now);
  formattedDate.value = formatter.format(now);
}

onMounted(async() => {
  await locomotive();
  setInterval(haveLocalTime, 1000);
})

</script>

<style scoped>
.wrapper{
  width: 100%;
  /* height: 100vh; */
  position: relative;
}

.hero-wrapper{
  width: 100%;
  height: 100vh;
  position: relative
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
  transform: translate(-50%);
  left: 50%;
  width: 50%;
  max-width: 40vw;
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
  /* width: 100%; */
  height: 100vh;
  left: 50%;
  border-top-right-radius: 50%;
  border-top-left-radius: 50%;
  -webkit-transform: scale(1) translateX(-50%);
  transform: scale(1) translateX(-50%);
  -webkit-transform-origin: center center;
  transform-origin: center center;
  z-index: 0;
}

.main{
  height: max-content;
  width: 100%;
}

.bg{
  background-color: var(--black-color);
  width: 100%;
  height: max-content;
}

.wrapper-project{
  background-color: var(--black-color);
  width: 100%;
  height: 100vh;
  margin-top: 40vh;
  z-index: 4;
  position: relative;
}

.wrapper-competences{
  display: flex;
  flex-direction: column;
  width: 100%;
  color: white;
  margin-top: 10vh;
  justify-content: center;
  align-items: center;
}

.wrapper-competences .high,
.wrapper-competences .bottom{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  width: max-content;
  /* overflow: auto; */
  gap: 5vw;
}

.wrapper-competences .high{
  justify-content: center;
  align-items: center;
}

.wrapper-competences span{
  font-family: "Dahlia";
  font-size: 90px;
}

.wrapper-infos{
  width: 100%;
  min-height: 100vh;
  max-height: 100vh;
  transition: all 0.3s linear;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.wrapper-infos h3{
 font-family: "Dahlia";
 text-align: center;
 font-size: 80px;
}

.container-titleInfos{
  position: relative;
  z-index: 3;
}

.container-titleInfos svg{
  position: absolute;
  top: 15%;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  z-index: -1;
}

.container-infos{
  width: max-content;
  height: 100%;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-size: 90px;
  font-weight: 600;
  font-family: "Inter", sans-serif;
}

.row-infos{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.row-infos p{
  margin: 0;
}

.row-infos a{
  text-decoration: none;
  color: black;
}

.telNumber span{
  transition: all 0.2s linear;
}

.telNumber:hover span:nth-child(even){
  transition: all 0.2s linear;
  transform: translate3d(-3px, -30px, 0);
  rotate: 10deg;
}

.telNumber:hover span:nth-child(odd){
  transition: all 0.2s linear;
  transform: translate3d(3px, 30px, 0);
  rotate: -10deg;
}

footer{
  width: 100%;
  height: 100%;
}

.footer-section{
  width: 100%;
  color: white;
  height: 100vh;
  background-color: var(--black-color);
}

.container-hello{
  width: 100%;
  text-align: center;
  display: flex;
  flex-direction: column;
  position: relative;
}

.bottom-section{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  bottom: 0;
}

.container-bottom{
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: end;
  margin-right: 5vw;
}

.container-bottom p{
  margin: 0;
}

.hello{
  font-size: 430px;
  font-family: 'Inter';
  font-weight: bold;
  text-transform:uppercase;
  margin: 0;
  position: absolute;
  transform: translate(-50%);
  left: 50%;
  opacity: 0.2;
}

.feel{
  position: absolute;
  transform: translate(-50%);
  left: 50%;
  top: 35vh;
  color: var(--active-color);
  font-weight: bold;
  font-size: 50px;
  width: 100%;
}

.container-contact{
  /* padding: 1% 5%; */
  width: 20%;
  height: 5vh;
  background-color: var(--active-color);
  border-radius: 12px;
  text-transform: uppercase;
  margin-bottom: 10vh;
  transition: all 0.2s linear;
  color: white;
  font-weight: 500;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  transition: all 0.2s linear;
}

.container-contact::before{
  content: "-->";
  opacity: 0;
}

.container-contact::after{
  content: "-->";
  opacity: 0;
  transition: all 0.2s linear;
}

.container-contact:hover::after{
  opacity: 1;
  margin-left: 10%;
}

.rs{
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  width: 10%;
  gap: 2vw;
}

.rs a{
  text-decoration: none;
  color: white;
}

.footer-name{
  font-family: 'Dahlia';
  font-size: 35px;
}

.date{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 5vw;
}

.date p{
  margin: 0;
  font-weight: bold;
  font-size: 20px;
}
</style>
