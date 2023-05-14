<template>
    <TheHeader></TheHeader>
    <GameContent></GameContent>
</template>

<script>
import TheHeader from './components/Header/TheHeader.vue';
import GameContent from './components/Content/GameContent.vue'
export default {
  name: 'App',
  components:{
    TheHeader,
    GameContent,
  }
}
</script>

<style>
body{
  margin:0;
  padding:0;
  background-color: white;
  background-image: url("./bg.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
}
</style>
