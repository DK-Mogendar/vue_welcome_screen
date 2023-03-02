<template>
  <div id="app">
    <h1 class="site-title">{{ title }}</h1>
    <span class="site-description">{{ currentDate }}</span>

    <!-- entry list -->
    <ul v-if="entries" class="entry-list" >
      <li v-for="entry in entries" class="entry-item"  :key="entry.id">
        <span class="entry-daytime">02/03/2023 {{entry[1] }} {{entry[0] }} Uhr</span><br />
        <h3 class="entry-title">{{ entry[2]}}</h3>
        <span class="entry-description">{{ entry[3]}}</span><br />
      </li>
    </ul>

    <!--Text wird nur angezeigt wenn keine einträge vorhanden-->
    <h1 v-else>Keine Events zur Zeit vorhanden!</h1>

    <!-- footer -->
    <footer class="footer">
      <img
        src="./assets/STZH_SEB_Logo.png"
        alt="Stadt Zürich Soziale Betriebe Logo"
      >
      <img
        src="./assets/Opportunity.png"
        alt="Opportunity Zürich Logo"
      >
      <img
        src="./assets/SAG_Logo_De.png"
        alt="Stiftung Arbeitsgestaltung Logo"
      >
    </footer>
  </div>
</template>

<script>

export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      currentDate: "",
      entries: []
    };
  },

  methods: {
    getData() {
      this.entries =  [
        ["8:25", "08/09/2022", "Auaaa wirklich", "Alles zum thema Auaaaaaa"],
        ["17:25", "07/03.2023", "Coole sache", "alles zu Cool"],
        ["17:25", "07/03.2023", "Coole sache", "alles zu Cool"]
      ];
    },
    updateCurrentDate() {
      let today = new Date();
      this.counter++;
      this.currentDate = `${today.getDate()}.${today.getMonth() + 1}.${today.getFullYear()}`;
    },
    refreshData() {
      this.updateCurrentDate();
      this.getData();
    },
  },
  mounted() {
    this.refreshData(); // get first initial data and then wait for the next
    setInterval(this.refreshData, 60000); // wait one minute for next update (1000 * 60)
  },
};
</script>

<style>

@import url("https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22");

body{
background-color:#e8eff4;
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
.site-title {
  color: black;
  font-size: 62px;
  font-weight: 900;
  margin: 80px 0 20px 0;
}

.site-description{
  color:#9AA7B1;
  font-size: 62px;
  color: #9aa7b1;
  font-weight: 500;
  margin: 0;
  
}
.entrie {
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
