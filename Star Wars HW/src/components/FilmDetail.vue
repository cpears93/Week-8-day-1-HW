<template lang="html">
  <div v-if="film" id="filmDetail">
    <div id="detailWrapper">
      <div id="flexWrapper">
        <div id="left">
          <h2>{{film.name}}</h2>
          <p><span>Title</span>: {{film.title}}</p>
          <p><span>Episode Number</span>: {{film.episodeNumber}}</p>
          <p><span>Release Date</span>: {{film.releaseDate}}
          <p><span>Director</span>: {{film.director}}</p>
          <p><span>Character Name</span>: {{film.characterName}}</p>
          <p><span>Height</span>: {{film.characterHeight | toFixed (2) }}</p>
        </div>
        <div id="right">
          <img id="film-image" :src="film.image" :alt="film.name">
        </div>
      </div>
    </div>

    <div id="episode-list-wrapper">
      <episode-list v-if="episodes.length" :episodes="episodes" ></episode-list>
  </div>

</div>
</template>

<script>
import EpisodeList from './EpisodeList.vue';

export default {
  name: 'film-detail',
  props: ['film'],
  components: {
    'episode-list': EpisodeList
  },
  data() {
    return {
      episodes: []
    }
  },
  methods: {
    getEpisodes() {
      const episodePromises = this.film.episode.map((episodeUrl) => {
        return fetch(episodeUrl).then(response => response.json())
      })
      Promise.all(episodePromises)
        .then(data => this.episodes=data)
    }
  },
  mounted(){
    this.getEpisodes();
  },
  watch: {
    film: function(){
      this.getEpisodes();
    }
  }
}
</script>

<style lang="css" scoped>
#filmDetail {
  box-sizing: border-box;
  height: 100%;
  width: 60%;
  background: #eee;
  color: #222;
  padding: 10px;
  border: 1px solid #ccc;
  display: flex;
}

#detailWrapper {
  box-sizing: border-box;
  background: #fff;
  padding: 10px;
  height: 100%;
  border-radius: 3px;
}

#flexWrapper {
  display: flex;
  justify-content: space-between;
}

#left, #right {
  width: 45%;
}

#right img {
  width: 100%;
}

#left p:first-child {
  margin-top: 0;
}

h2 {
  margin: 10px 0 20px;
  padding: 0;
}

p span {
  font-weight: bold;
}

#episode-list-wrapper{
  width: 50%;
  display: flex;
  justify-content: center;
}

#film-image {
  height: 300px;
}

</style>
