<template>
    <div id="nav">
        <router-link to="/">
            <img id="logo" :src="logo" :alt="alt">
        </router-link>
        <div>
            <router-link to="/">Home</router-link>
            <router-link to="/pedidos">Pedidos</router-link>
        </div>
    </div>
</template>

<script>
export default {
    name:"Header",
    props:["logo", "alt"]
}
</script>

<style scoped>
    #nav{
        background-color: #0e0e0e;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1.2rem;
    }

    #logo{
        width: 80px;
        height: 80px;
    }

    #nav a{
        text-decoration: none;
        
        font-size: 1.4rem;
        margin: 1rem;
        transition: 0.3s ease-in-out;
    }

    #nav a:hover{
        color: #fffff0;
    }
</style>