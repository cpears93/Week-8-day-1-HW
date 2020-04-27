<template lang="html">
  <div v-if="episodes" class="episode-list">
    <h3>Episode List</h3>
    <ul>
      <episode-list-item v-for="(episode, index) in episodes" :key="index" :episode="episode"></episode-list-item >
    </ul>
  </div>
</template>

<script>

import EpisodeListItem from './EpisodeListItem'
export default {
  name: 'episode-list',
  props: ['episodes'],
  components: {
    'episode-list-item': EpisodeListItem
  }
}
</script>

<style lang="css" scoped>

.episode-list {
  width: 100%;
  text-align: center;
}
</style>
