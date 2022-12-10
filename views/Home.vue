<template>
    <Banner/>
    <div class="main_container">
        <h1>Escolha sua Pizza:</h1>
    </div>
</template>

<script>
import Banner from "../components/Banner.vue"

export default {
    name: "Home",
    components:{
        Banner
    }
}
</script>

<style scoped>
.main_container{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1.2rem;
}
</style>