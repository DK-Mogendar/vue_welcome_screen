<template>
    <span class="entry-daytime">{{entry[0]}} Uhr, {{entry[1].replaceAll("/", ".")}}</span><br />
    <h3 class="entry-title">{{entry[2]}}</h3>
    <span class="entry-description">{{entry[3]}}</span><br />
</template>

<script>
export default {
  props: ['entry'],
  data() {
    return {
      // counter: 0
    }
  }
}
</script>