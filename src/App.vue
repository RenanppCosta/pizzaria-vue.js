<template>
      <Header :logo="logo_src"  :alt="app_name" />
      <router-view></router-view>
      <Footer />
</template>

<script>
import Header from "../components/Header.vue"
import Footer from "../components/Footer.vue"

export default {
  components:{
    Header,
    Footer
  },
  data(){
    return{
      logo_src: "img/pizza.png",
      app_name: "Pizzaria.Vue"
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap');

*{
  font-family: "Quicksand";
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
