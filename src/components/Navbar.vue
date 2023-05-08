<template>
    <nav ref="navbar" class="nav-wrapper">
        <div class="nav-left">
            <h1>
                Lucas Huerta
            </h1>
        </div>
        <div class="nav-right">
            <p @click="scrollWorks()">
                Works
            </p>
            <p @click="scrollContact()">
                Contact
            </p>
        </div>
    </nav>
</template>

<script setup>
import { ref } from 'vue';

const emits = defineEmits(['scrollProject', 'scrollContact'])
let navbar = ref();

const scrollWorks = () => {
    emits('scrollProject');
}

const scrollContact = () => {
    emits('scrollContact');
}
</script>

<style scoped>

.nav-wrapper{
    background-color: white;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: fit-content;
    padding-bottom: 20px;
    border-bottom: 2px solid black;
    padding-top: 2vh;
    text-transform: uppercase;
    z-index: 10;
    position: fixed;
}
.nav-right{
    display: flex;
    flex-direction: row;
}

.nav-left h1{
    font-size: 30px;
    margin: 0 2vw;
}

.nav-left{
    display: flex;
    flex-direction: row;
    justify-content: right;
}

.nav-right p{
    margin: 0 2vw;
    font-size: 20px;
    cursor: pointer;
}

</style>