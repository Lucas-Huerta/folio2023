<template>
    <div class="container-project">
        <div class="project" @mouseover="showImage" @mouseleave="hideImage">
            <div class="left-project">
                <span>
                    {{props.projet.tag}}
                </span>
                <h3>{{props.projet.nom}}</h3>
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
const offset = 20;
let projectImg = ref();

const showImage = async(event) => {
    show.value = true;
    mouseX.value = await event.clientX;
    mouseY.value = await event.clientY;
    projectImg.value.style.right = mouseX.value % 10 + '%';
    projectImg.value.style.top = mouseY.value % 10 + '%';
}

const hideImage = () => {
    show.value = false;
}

</script>

<style scoped>
.container-project{
    display: flex;
    flex-direction: column;
    width: 100%;
    color: white;
    justify-content: space-evenly;
    align-items: center;
    margin-top: 10vh;
}

.project{
    position: relative;
    width: 80%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    transition: all 1s;
    border-bottom: 1px solid rgba(255, 255, 255, 0.171);
}

.project:hover{
    border-bottom: 1px solid white;
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