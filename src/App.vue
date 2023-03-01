<template>
  <HelloWorld msg="Welcome to Opportunity"/>
 
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}

</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22");
body{
background-color:#E5E5E5;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align:start;

  margin-top: 60px;
}
.titel {
    margin: 30px;
    padding: 20px;
    font-weight:500;
    font-Size:28px;
    line-height:36px;
    Font:Inter;
    font-Weight:900;
    Size:28px;
    Line-height:36px;
}
.app {
    margin: 30px;
    padding: 20px;
    background-color: rgb(34, 13, 109); 
    color: aliceblue;
    font-weight:500;
    font-Size:28px;
    line-height:36px;
    Font:Inter;
    font-Weight:900;
    Size:28px;
    Line-height:36px;
  }
.farbe1 {
    color:#EB5E00;
  }
.farbe2 {
    color:#FFBFAB;
  }
.farbe3 {
    color:#FFBFAB;
  }

.t1 {
    color: black;
  }
.t2 {
    color:#9AA7B1;
  }

.footer {
    background-color: white;
  }
.flex-container {
  display: flex;
}

.flex-container img {
  flex-basis: 100%;
  max-width: 33%;
  height: auto;
}

</style>
