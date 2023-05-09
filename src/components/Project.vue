<template>
    <div class="container-project">
        <div class="project" @mouseover="showImage" @mouseleave="hideImage" @click="clickProject()" ref="rowProject">
            <div class="row" ref="row" style="flex-direction: row; align-items: flex-end;">
                <div class="left-project">
                    <span>
                        {{props.projet.tag}}
                    </span>
                    <h3>{{props.projet.nom}}</h3>
                </div>
                <div class="infosSupp" ref="infosSupp" style="opacity: 0;">
                    <p style="margin-top: 0;">
                        {{props.projet.description}}
                    </p>
                    <!-- <img :src="projet.image"> -->
                </div>
            </div>
            <div class="right-project">
                <span class="col-comp" v-for="comp in props.projet.competences">{{ comp }}</span>
                <img :src="projet.image" class="project-image" v-show="show" ref="projectImg">
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    projet: Object
})

const show = ref(false);
const mouseX = ref(0);
const mouseY = ref(0);
let projectImg = ref();
let infosSupp = ref();
let row = ref();

/**
 * Permet de show l'image projet et de lui assigner les coordonées x et y de la row projet 
 * @param {*} event event lors de l'hover projet
 */
const showImage = async(event) => {
    show.value = true;
    mouseX.value = await event.clientX;
    mouseY.value = await event.clientY;
    projectImg.value.style.right = mouseX.value % 10 + '%';
    projectImg.value.style.top = mouseY.value % 10 + '%';
}

/**
 * Unshow l'image projet
 */
const hideImage = () => {
    show.value = false;
}

const clickProject = () =>{
    if (infosSupp.value.style.opacity == '0') {
        infosSupp.value.style.opacity = '1';
        infosSupp.value.style.width = '100%';
        row.value.style.flexDirection = 'column';
        row.value.style.alignItems = 'start';
    }else{
        setTimeout(() =>{
            row.value.style.transition = 'all 1s';
            row.value.style.flexDirection = 'row';
            infosSupp.value.style.width = '50%';
            row.value.style.alignItems = 'flex-end';
        }, 1000);
        infosSupp.value.style.opacity = '0';
    }
}

</script>

<style scoped>
.container-project{
    display: flex;
    flex-direction: column;
    width: 100%;
    height: max-content;
    color: white;
    justify-content: space-evenly;
    align-items: center;
    margin-top: 10vh;
}

.infosSupp{
    width: 50%;
    display: flex;
    justify-content: space-between;
    transition: opacity 1s linear;
}

.infosSupp p {
   margin-top: O;
   width: 90%;
}

/* .infosSupp img {
    width: 50%;
    height: auto;
} */

.project{
    position: relative;
    width: 80%;
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    transition: all 1s;
    border-bottom: 1px solid rgba(255, 255, 255, 0.171);
}

.project .row{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}

.project:hover{
    border-bottom: 1px solid white;
    cursor: pointer;
}

.clickProject{
    transition: all 1s;
    height: 20vh;
    width: 80%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}

.left-project{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.left-project span{
    font-size: 15px;
    padding: 2px 2vw;
    background-color: var(--active-color);
    border-radius: 12px;
}

.left-project h3{
    font-family: "Dahlia";
    font-weight: lighter;
    letter-spacing: 5px;
    font-size: 40px;
    margin: 0;
}

.right-project{
    width: 20%;
}

.col-comp{
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: center;
    color: white;
}

.project-image{
    position: absolute;
    /* top: 0;
    left: 40%; */
    max-width: 300px;
    max-height: 300px;
}
</style>