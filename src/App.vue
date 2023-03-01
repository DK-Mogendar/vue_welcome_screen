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
  font-family: "inter", Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #323d4a;
  margin-top: 60px;
}
.header {
  margin: 30px;
}
.title {
  font-size: 62px;
  font-weight: 900;
  margin: 80px 0 20px 0;
}

.untertitel{
  font-size: 62px;
  color: #9aa7b1;
  font-weight: 500;
  margin: 0;
  
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
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 40px;
  background: #FFFFFF;
  }
.footer img {
  height: 50px;
}

</style>
