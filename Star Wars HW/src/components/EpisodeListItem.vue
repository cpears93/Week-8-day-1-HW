<template lang="html">
  <li>{{episode.name}}</li>
</template>

<script>
export default {
  name: 'episode-list-item',
  props: ['episode']
}
</script>

<style lang="css" scoped>

li {
  list-style: none;
  color: darkslategrey;
  line-height: 1.4;
  font-size: 1.2em;
  width:100%;
}
</style>
