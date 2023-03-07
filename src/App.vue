<template>
  <div id="app"> <!--Uebergeortneter Div über das gesamte Template (wird genutzt um übergeortnete css Styles zu vergeben)-->
    <h1 class="site-title">{{ title }}</h1> <!--Gibt den Titel aus-->
    <span class="site-description">{{ currentDate }}</span><!--Gibt das aktuelle Datum aus-->

    <!-- entry list -->
    <!--v-if ist eine vue.js definition für if( If bedingung)-->
    <!-- Schleife durch alle Einträge in entries -->
    <ul v-if="entries && entries.length" class="entry-list" >
      <li class="entry-item"  v-for="entry in entries" :key="entry.id">
        <!-- Rendere einen einzelnen Eintrag mit dem EventEntry-Komponenten-Tag -->
        <EventEntry :entry="entry"/>
      </li>
    </ul>

    <!--Text wird nur angezeigt wenn keine einträge vorhanden.-->
    <h1 v-else>Keine Events zur Zeit vorhanden!</h1>

    <!-- footer -->
    <!--Enthält nur drei bilder die im Footer angezeigt werden.-->
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
import EventEntry from "./components/EventEntry.vue";

//Definiert dei einzelnen Variablen der App
export default {
    name: "App",
    components: { EventEntry },
    data() {
        return {
            title: "Welcome to Opportunity",
                                 /*Meine Liste */                          /*Chris Liste */
            sheet_id: "1ycTdsvR4P08qDw9p0rmN73rqtqdXGdwxYDLKEGgEnpc" /*"1CR1UKN0LAPNs6lWbfA2gBI2FazmWdVSFIzIwi5TG5Z4"*/,
            api_token: "AIzaSyAcQYdWwMV5KCzZIKI-gozSS9osnZ5CQsE" /*"AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU"*/,
            currentDate: "",
            entries: []
        };
    },
    computed: {
        /*Dieser Code definiert eine Eigenschaft gsheet_url, die eine URL zurückgibt, die auf eine bestimmte Tabelle
        in einer Google Sheets-Datei verweist. Die URL wird mit den Informationen sheet_id und api_token generiert,
        die von der Klasse verwendet werden, in der sich dieser Code befindet.
        (ChrisBeschreibung).
        Berechnete Eigenschaften sind wie Dateneigenschaften,
        aber mit einer kombinierten Methode, die automatisch ausgeführt wird, anstatt explizit eine Funktion aufzurufen. */
        gsheet_url() {
            return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2:E100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
        },
    },
    methods: {
        //Alte version

        /*Beginn mit der
        Funktion getData()
        Rufen Sie axios.get() mit this.gsheet_url als Argument auf.
        Warted auf die Antwort.
        Wenn die Antwort erfolgreich ist, dann
        setze this.entries auf die Werte des ersten Wertebereichs in response.data
        ENDWENN
        ENDFUNKTION
        END*/

        /* getData() {  
              axios.get(this.gsheet_url).then((response) => {
                  this.entries = response.data.valueRanges[0].values;
              });
        },*/

        //Neue Version mit sortierung na aubgelaufenen Datum un daussortierung

        /*Beginn mit der
        Funktion getData()
        Rufen Sie axios.get() mit this.gsheet_url als Argument auf.
        Warted auf die Antwort.
        Wenn die Antwort erfolgreich ist, dann
        setze this.entries auf die Werte des ersten Wertebereichs in response.data
        ENDWENN
        ENDFUNKTION
        END*/
        getData() {
          axios.get(this.gsheet_url).then((response) => {
            // Erhalte die Zeilen aus der Antwort des API-Aufrufs
            const rows = response.data.valueRanges[0].values;
            // Erhalte das aktuelle Datum
            const currentDate = new Date();
            // Filtere die Zeilen, die ein Datum haben, das heute oder später ist
            const filteredRows = rows.filter(row => {
              // Zerlege das Datum in seine Teile
              const dateParts = row[1].split("/");
              // Erstelle ein neues Datum aus den Datumsteilen
              const rowDate = new Date(`${dateParts[2]}-${dateParts[1]}-${dateParts[0]}`);
              // Vergleiche das neue Datum mit dem aktuellen Datum und gib das Ergebnis zurück
              return rowDate >= currentDate;
            });
             // Sortiere die gefilterten Zeilen nach Datum
            this.entries = filteredRows.sort((row1, row2) => {
              // Zerlege die Datumsteile des ersten Datums (uhr Zeit)in row1
              const dateParts1 = row1[1].split("/");
              // Zerlege die Datumsteile des zweiten Datums (Kalender) in row2
              const dateParts2 = row2[1].split("/");
              // Erstelle neue Datumobjekte aus den Datumsteilen beider Zeilen
              const date1 = new Date(`${dateParts1[2]}-${dateParts1[1]}-${dateParts1[0]}`);
              const date2 = new Date(`${dateParts2[2]}-${dateParts2[1]}-${dateParts2[0]}`);
              // Vergleiche die Datumobjekte und gib das Ergebnis zurück
              return date1 - date2;
            });
          });
        },
        
        //Altes Beispiel hier scheiben wie das Datum und die Uhrzeit als Numerischen String(Kein richtiges Datum)
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
    }
};
</script>

<style>
/* Importiert die Schrift art */
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22");

body{
background-color:#e8eff4;
}
#app {
  font-family: "inter", Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
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
