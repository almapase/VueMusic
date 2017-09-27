<template lang="html">
  <li class="artist">
    <h2><a :href="artist.url" target="_blank">{{ artist.name }}</a></h2>
    <img :src="artist.image[2]['#text']" :alt="artist.name">
  </li>
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<style lang="css" scoped>
li.artist{
  display: inline-table;
  margin: 10px 10px;
}
</style>
