<template>
    <nav class="nav-wrapper">
        <div class="nav-left">
            <h1>
                Lucas Huerta
            </h1>
        </div>
        <div class="nav-right">
            <p>
                Works
            </p>
            <p>
                Contact
            </p>
        </div>
    </nav>
</template>

<script setup>
</script>

<style scoped>

.nav-wrapper{
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
}

</style>