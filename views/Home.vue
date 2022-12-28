<template>
    <Banner />
    <div class="main_container">
        <h1>Escolha sua Pizza:</h1>
        <Form />
    </div>
</template>

<script>
import Banner from "../components/Banner.vue"
import Form from "../components/Form.vue"

export default {
    name: "Home",
    components:{
        Banner,
        Form
    }
}
</script>

<style scoped>
.main_container{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 1.2rem;
}
</style>