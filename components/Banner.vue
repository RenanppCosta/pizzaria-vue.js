<template>
    <div id="main_banner">
        <h1>Pizzaria VueJS</h1>
    </div>
</template>

<script>
export default {
    name:"Banner"
}
</script>

<style scoped>
#main_banner{
    background-image: url("/img/background-pizza.jpg");
    background-size: cover;
    height: 600px;
    display: flex;
    align-items: center;
    justify-content: end;
}

#main_banner h1{
    font-size: 3rem;
    color:#ffed00;
    margin-right: 4rem;
}

@media(max-width:800px){
    #main_banner h1{
    display: none;
}
}
</style>