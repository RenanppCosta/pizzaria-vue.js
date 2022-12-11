<template>
   <div class="message_container">
    <p>{{msg}}</p>
   </div>
</template>

<script>

export default {
    name: "Message",
    props:{
        msg: String
    }
    
}
</script>

<style scoped>
    .message_container{
        background-color: #db7093;
        color: #ce3b6b;
        padding: 1rem;
        margin: 1rem;
    }
</style>