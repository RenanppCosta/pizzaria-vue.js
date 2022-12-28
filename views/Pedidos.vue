<template>
    <div class="main_container">
        <h1>Gerenciar Pedidos</h1>
        <Dashboard />
    </div>
</template>

<script>
import Dashboard from "../components/Dashboard.vue"

export default {
    name:"Pedidos",
    components:{
        Dashboard
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