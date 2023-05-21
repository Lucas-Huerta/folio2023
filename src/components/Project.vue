<template>
    <div class="container-project">
        <div class="project" @mousemove="showImage" @mouseleave="hideImage" @click="clickProject()" ref="rowProject">
            <img :src="projet.image" class="project-image" v-show="show" ref="projectImg" />
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
                </div>
            </div>
            <div class="right-project" ref="right">
                <span class="col-comp" v-for="comp in props.projet.competences">{{ comp }}</span>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    projet: Object
})

let rowProject = ref();
const show = ref(false);
const mouseX = ref(0);
const mouseY = ref(0);
let projectImg = ref();
let infosSupp = ref();
let row = ref();
let right = ref();

/**
 * Permet de show l'image projet et de lui assigner les coordonées x et y de la row projet 
 * @param {*} event event lors de l'hover projet
 */
const showImage = async(event) => {
    const parentRect = rowProject.value.getBoundingClientRect();
    show.value = true;
    mouseX.value = await event.clientX - parentRect.left;
    mouseY.value = await event.clientY - parentRect.top;
    
    projectImg.value.style.left = `${(mouseX.value / parentRect.width) * 100}%`;
    projectImg.value.style.top = `${(mouseY.value / parentRect.height) * 100}%`;
}

/**
 * Unshow l'image projet
 */
const hideImage = () => {
    show.value = false;
}

/**
 * Au clic sur la section projet => changement des styles sur les refs associées afin de montrer la description du projet
 */
const clickProject = () =>{
    if (infosSupp.value.style.opacity == '0') {
        infosSupp.value.style.opacity = '1';
        infosSupp.value.style.width = '100%';
        row.value.style.flexDirection = 'column';
        row.value.style.alignItems = 'start';
        right.value.style.marginBottom = '2%';
    }else{
        // Comme la transition dure 1s, un timeout d'1s est assigné afin de ne pas voir le changement de style
        setTimeout(() =>{
            row.value.style.transition = 'all 1s';
            row.value.style.flexDirection = 'row';
            infosSupp.value.style.width = '65%';
            row.value.style.alignItems = 'flex-end';
        }, 1000);
        infosSupp.value.style.opacity = '0';
        right.value.style.marginBottom = '0';
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
}

.project{
    position: relative;
    width: 80%;
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-end;
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
    text-transform: uppercase;
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
    transition: all 1.5s;
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
    transition: all 0,2s linear;
}
</style>