<template>
  <q-page class="q-pa-md" v-if="game">
    <div class="row">
            <div class="col-12">
                <div class="q-pa-md q-gutter-sm">
                 <q-breadcrumbs>
                    <q-breadcrumbs-el icon="home" to="/" />
                    <q-breadcrumbs-el label="Juegos" icon="games" to="/games" />
                    <q-breadcrumbs-el :label="game.name" icon="videogame_asset" />
                </q-breadcrumbs>
    </div>
            </div>
        </div>
    <div class="row rowTitle">
            <div class="col-12">
                <h3>{{game.name}}</h3>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <img :src="game.background_image" class="imageGameView"/>
            </div>
        </div>
        <div class="row basicInfoGamesView">
        <div class="col-12 col-sm-12 col-md-4 col-lg-4 gameListDate">
                <div class="col-12">
                    <q-icon name="event" /><span>{{game.released}}</span>
                </div>
          </div>
        </div>
        <div class="col-12 col-sm-12 col-md-4 col-lg-4 gameListMetacritic">
                <div class="col-12">
                    <img src="~assets/metacritic.png"/><span>{{game.metacritic}}</span>
                </div>
           </div>
           <div class="col-12 col-sm-12 col-md-4 col-lg-4 gameListPlayTime">
                <div class="col-12">
                     <q-icon name="schedule" /><span>{{game.playtime}} horas</span>
                </div>
            </div>
            <div class="row">
            <div class="col-12">
                <div class="q-pa-md">
                    <q-rating
                        v-model="game.rating"
                        max="5"
                        size="3.2em"
                        color="yellow"
                        icon="star_border"
                        icon-selected="star"
                        icon-half="star_half"
                        no-dimming
                        readonly
                    />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <span v-for="(platform, index) in game.platforms" :key="platform.platform.id">
                    <span v-if="index !== 0">-</span>
                        {{platform.platform.name}}
                </span>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <span v-for="genre in game.genres" :key="genre.id">
                    <q-icon name="label" /> {{genre.name}}
                </span>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <span>Comprar en: </span>
                <span v-for="(store, index) in game.stores" :key="store.store.id">
                    <span v-if="index !== 0">-</span>
                        <a v-if ="store.url_en" :href="store.url_en" target="_blank">{{store.store.name}}
                        </a>
                        <a v-if ="store.url" :href="store.url_en" target="_blank">{{store.store.name}}
                        </a>
                </span>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                    <q-chip color="secondary" text-color="white" icon="label" name="label" v-for="tag in game.tags" :key="tag.id">
                        {{tag.name}}
                    </q-chip>
            </div>
        </div>
        <div class="row carouselRow">
            <div class="col-12">
                <q-carousel
                    swipeable
                    animated
                    v-model="slide"
                    thumbnails
                    infinite
                    >
                    <q-carousel-slide name="video" :img-src="game.clip.preview">
                        <q-video class="absolute-full" :src="game.clip.clip" />
                    </q-carousel-slide>
                    <q-carousel-slide v-for="(image, index) in game.short_screenshots" :key="image.id" :name="index" :img-src="image.image" />
                </q-carousel>
            </div>
        </div>
   </q-page>
</template>

<script>
export default {
  name: 'GamesView',
  data () {
    return {
      slide: 0,
      game: null
    }
  },
  async created () {
    if (this.gamepass === null || this.gamepass === undefined) {
      await this.$axios.get('https://api.rawg.io/api/games/' + this.id).then((response) => {
        this.game = response.data
      }).catch(() => {
        this.$q.notify({
          color: 'negative',
          position: 'top-right',
          message: 'Error al cargar el Juegos',
          icon: 'report_problem'
        })
      })
    } else {
      this.game = this.gamepass
    }
  },
  props: {
    id: {
      type: String,
      required: true
    },
    gamepass: {
      type: Object,
      required: false
    }
  },
  methods: {
    generateUrlStore (store) {
      var result = ''
      if (store !== null && store.url_en !== null) {
        result = store.url_en
      } else if (store !== null && store.url !== null) {
        result = store.url
      }
      return result
    }
  }
}
</script>
