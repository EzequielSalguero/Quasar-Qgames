<template>
    <div class="row rowFilter">
        <div class="col-12 col-sm-12 col-md-2 col-lg-2 filterText">
            <q-input v-model="search" label="Filtro por titulo" placeholder="MetalGear... por ejemplo"/>
        </div>
        <div class="col-12 col-sm-12 col-md-2 col-lg-3 filterSelect">
            <q-select multiple v-model="genre" :options="genresOptions" label="Filtro por género" placeholder="Selecciona genero" option-value="id" option-label="name" emit-value map-options/>
        </div>
        <div class="col-12 col-sm-12 col-md-2 col-lg-3 filterSelect">
            <q-input v-model="fecha" label="Filtro por fecha" readonly>
            <template v-slot:append>
                <q-icon name="event" class="cursor-pointer">
                    <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
                        <q-date v-model="range" range></q-date>
                    </q-popup-proxy>
                </q-icon>
        </template>
      </q-input>
        </div>
        <div class="col-12 col-sm-12 col-md-6 col-lg-6 filterButton">
            <q-btn color="dark" icon-right="settings_backup_restore" label="LIMPIAR" @click="limpiar"/>
            <q-btn color="primary" icon-right="search" label="BUSCAR" @click="buscarEnComponente"/>
        </div>
     </div>
</template>

<script>
export default {
  name: 'GamesListFilter',
  data () {
    return {
      search: null,
      genre: null,
      genresOptions: null,
      date: null,
      range: null,
      fecha: ''
    }
  },
  created () {
    this.loadGenres()
  },
  watch: {
    range: function (val) {
      console.log(val)
      var dateFrom = new Date(val.from)
      var dateTo = new Date(val.to)
      this.date = val.from.replaceAll('/', '-') + ',' + val.to.replaceAll('/', '-')
      this.fecha += 'Desde: ' + dateFrom.getDate() + '-' + (dateFrom.getMonth() + 1) + '-' + dateFrom.getFullYear() + ' hasta: ' + dateTo.getDate() + '-' + (dateTo.getMonth() + 1) + '-' + dateTo.getFullYear()
    }
  },
  methods: {
    limpiar () {
      this.genre = null
      this.search = null
      this.date = null
      this.range = null
      this.fecha = ''
      this.buscarEnComponente()
    },
    buscarEnComponente () {
      this.$emit('filtrar', this.search, this.genre, this.date)
    },
    async loadGenres () {
      var url = 'https://api.rawg.io/api/genres?page_size=99'
      await this.$axios.get(url).then((response) => {
        this.genresOptions = response.data.results
      }).catch(() => {
        this.$q.notify({
          color: 'negative',
          position: 'top-right',
          message: 'Error al cargar los generos',
          icon: 'report_problem'
        })
      })
      console.log(this.genresOptions)
    }
  }
}
</script>
