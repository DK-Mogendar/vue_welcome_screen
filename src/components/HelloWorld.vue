<template>
  

    
    <header>
      <div class="titel">
        <h1 class="t1">{{ msg }}</h1>
        <h1 class="t2">01.03.2023</h1>
      </div>
    </header>

<section>
  
  <div class="app">
        <ul>
          <li class="farbe1">14.00 UHR</li><br>
          <li class="farbe2">Basisbeschäftingung Besuch</li><br>
          <li class="farbe3">Interessierte für den zweiten Kurs</li><br>
        </ul>
      </div>

    
      <div class="app">
        <ul>
          <li class="farbe1">14.00 UHR</li><br>
          <li class="farbe2">Basisbeschäftingung Besuch</li><br>
          <li class="farbe3">Interessierte für den zweiten Kurs</li><br>
        </ul>
      </div>

      <div class="app">
        <ul>
          <li class="farbe1">14.00 UHR</li><br>
          <li class="farbe2">Basisbeschäftingung Besuch</li><br>
          <li class="farbe3">Interessierte für den zweiten Kurs</li><br>
        </ul>
      </div>
    </section>

  

    <footer class="footer">

    
        <img src="../assets/STZH_SEB_Logo.png" alt="Bild 1">
        <img src="../assets//Opportunity.png" alt="Bild 2">
        <img src="../assets/SAG_Logo_De.png" alt="Bild 3">

     </footer>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
