<template>
<div class="app">
  <Home />
</div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Chivo:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap');
*{
  font-family: 'chivo';
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.app{
  background: url(./assets/bg.png);
  height: 100vh;
  width: 100%;
  background-size: cover;
  background-color: rgb(0, 0, 0);
  padding: 5vh 2vw;


}
</style>
