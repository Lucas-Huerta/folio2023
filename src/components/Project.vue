<template>
    <div class="container-project">
        <div class="project">
            <div class="left-project">
                <span>
                    {{props.projet.tag}}
                </span>
                <h3>{{props.projet.nom}}</h3>
            </div>
            <div class="right-project">
                <img src="" alt="image project">
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted } from 'vue';

const props = defineProps({
    projet: Object
})

onMounted(() => {
})
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
</style>