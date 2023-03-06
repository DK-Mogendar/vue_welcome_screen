<template>
  <div id="app">
    <h1 class="site-title">{{ title }}</h1>
    <span class="site-description">{{ currentDate }}</span>

    <!-- entry list -->
    <ul v-if="entries && entries.length" class="entry-list" >
      <li v-for="entry in entries" class="entry-item"  :key="entry.id">
        <span class="entry-daytime">{{entry[0] }} Uhr, {{entry[1].replaceAll("/", ".")}}</span><br />
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
import axios from "axios"; //axios is a libary for making HTTP rquest to the backend

//Definiert dei einzelnen Variablen der App
export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
                    /*Meine Liste */                                         /*Chris Liste */
      sheet_id:/*1ycTdsvR4P08qDw9p0rmN73rqtqdXGdwxYDLKEGgEnpc*/ "1CR1UKN0LAPNs6lWbfA2gBI2FazmWdVSFIzIwi5TG5Z4",
      api_token:/*"AIzaSyAcQYdWwMV5KCzZIKI-gozSS9osnZ5CQsE"*/"AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
      currentDate: "",
      entries: []
    };
  },

  computed: {
    // computed properties are like data properties, but with a method combined and it gets executed automatically, instead of calling a function explicitly
    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },

  methods: {
    getData() {
      /*BEGINN
      FUNKTION getData()
      Rufen Sie axios.get() mit this.gsheet_url als Argument auf.
      Warted auf die Antwort.
      Wenn die Antwort erfolgreich ist, dann
      setze this.entries auf die Werte des ersten Wertebereichs in response.data
      ENDWENN
      ENDFUNKTION
      END*/
      
        axios.get(this.gsheet_url).then((response) => {
          this.entries = response.data.valueRanges[0]. values;
        });
     

      /*this.entries =  [
        ["8:25", "08/09/2022", "Auaaa wirklich", "Alles zum thema Auaaaaaa"],
        ["17:25", "07/03.2023", "Coole sache", "alles zu Cool"],
        ["19:25", "08/03.2023", "Coole sache zwei", "alles zu Cool zwei"]
      ]; */

    /*Beginn mit der
    Funktion updateCurrentDate()
    setze today auf ein neues Datum-Objekt
    Inkementiere this.counter um 1
    setze this.currentDate auf einen String, der das heutige Datum im Format "Tag.Monat.Jahr" darstellt
    ENDFUNKTION
    END*/ 
    },
    updateCurrentDate() {
      let today = new Date();
      this.counter++;
      this.currentDate = `${today.getDate()}.${today.getMonth() + 1}.${today.getFullYear()}`;
    },

  /*Beginn mit der
  Funktion refreshData()
  ruf das updateCurrentDate() auf
  ruf das getData() auf
  ENDFUNKTION
  END */  
    refreshData() {
      this.updateCurrentDate();
      this.getData();
    },
  },

  /*Beginn mit der
  Funktion mounted()
  ruf das refreshData() auf, um die ersten Daten abzurufen und auf das nächste Update zu warten
  seze den Intervall-Timer auf, der alle 18000000 Millisekunden die refreshData() Methode ausführt
  ENDFUNKTION
  END */
  mounted() {
    this.refreshData(); // get first initial data and then wait for the next
    setInterval(this.refreshData, 18000000); // wait one minute for next update (1000 * 60)
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
  margin: 30px;
}

.site-title {
  font-size: 62px;
  font-weight: 900;
  margin: 80px 0 20px 0;
}

.site-description{
  font-size: 62px;
  color: #9aa7b1;
  font-weight: 500;
  margin: 0;

  
}
.entry-list {
  padding-left: 0;
}

.entry-item {
  padding: 35px 40px;
  margin: 40px 0;
  background: #0f05a0;
  font-size: 28px;
  line-height: 1.3;
  list-style: none;
}

.entry-daytime {
  color: #eb5e00;
  font-weight: 900;
}

.entry-title {
  font-size: inherit;
  margin: 0;
  color: #ffbfab;
  font-weight: 900;
}

.entry-description {
  color: #ffbfab;
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

</style>§
