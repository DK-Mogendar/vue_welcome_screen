<template>
    <!-- Anzeige der Tageszeit des Eintrags im 24-Stunden-Format plus das Datum-->
    <span class="entry-daytime">{{entry[0]}} Uhr, {{entry[1].replaceAll("/", ".")}}</span><br />
    <!--Anzeige des Titels-->
    <h3 class="entry-title">{{entry[2]}}</h3>
    <!--Anzeige der anstehenden Aufgabe-->
    <span class="entry-description">{{entry[3]}}</span><br />
</template>

<script>//Exportiert das Objekt vom vordefinierten Modul (Export-Objekt)
export default {
  //Props (Vue.js-Komponente) deklariert Parameter zur definition,von übergeordneten Komponenten die übergeben werden können.
  props: ['entry'],
  data() {//Giebt die zusammengestellten Daten aus.
    return {
      // counter: 0 (Altes Beispiel)
    }
  }
}
</script>