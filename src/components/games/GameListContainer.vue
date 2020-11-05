<template>
  <div class="gameListContainer" @click="viewGame">
    <div class="row">
          <div class="col-12 col-sm-12 col-md-12 col-lg-4 columnaListImagen">
            <img :src="game.background_image"/>
          </div>
          <div class="col-12 col-sm-12 col-md-12 col-lg-8 columnaListInfo">
              <div class="row gameListTitle">
                <div class="col-12">
                    {{game.name}}
              </div>
          </div>
          <div class="row gameListDate">
                <div class="col-12">
                    <q-icon name="event" /><span>{{game.released}}</span>
                </div>
          </div>
          <div class="row gameListMetacritic">
                <div class="col-12">
                    <img src="~assets/metacritic.png"/><span>{{game.metacritic}}</span>
                </div>
           </div>
           <div class="row gameListPlayTime">
                <div class="col-12">
                     <q-icon name="schedule" /><span>{{game.playtime}} horas</span>
                </div>
            </div>
          </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'GameListContainer',
  data () {
    return {
      search: null
    }
  },
  props: {
    game: {
      type: Object,
      required: true
    }
  },
  methods: {
    viewGame () {
      this.$router.push({ path: 'games/view/' + this.game.id, name: 'gamesView', params: { id: this.game.id.toString(), gamepass: this.game } })
    }
  }
}
</script>
