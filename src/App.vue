<template>
    <TheHeader></TheHeader>
</template>

<script>
import TheHeader from './components/Header/TheHeader.vue';
export default {
  name: 'App',
  components:{
    TheHeader,
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
