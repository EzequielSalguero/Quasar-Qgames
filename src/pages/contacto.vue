<template>
    <q-page class="q-pa-md">
      <div class="row">
            <div class="col-12">
                <div class="q-pa-md q-gutter-sm">
                 <q-breadcrumbs>
                    <q-breadcrumbs-el icon="home" to="/" />
                    <q-breadcrumbs-el :label="Contacto" icon="contact_support" />
                </q-breadcrumbs>
              </div>
            </div>
    </div>
        <div class="row rowTitle">
            <div class="col-12">
                <h3>Contacto</h3>
            </div>
        </div>
        <div class="row rowInputs">
            <div class="col-12 col-sm-12 col-md-5 col-lg-5">
                <q-input outlined v-model="email" label="Email" hint="Introduzca su email" placeholder="email@email.com" />
            </div>
            <div class="col-0 col-sm-0 col-md-2 col-lg-2"></div>
            <div class="col-12 col-sm-12 col-md-5 col-lg-5">
                <q-input outlined v-model="nombre" label="Nombre" hint="Introduzca su nombre" placeholder="xxx yyy zzz" />
            </div>
        </div>
        <div class="row rowInputs">
            <div class="col-12 col-sm-12 col-md-5 col-lg-5" >
                <q-input outlined v-model="tlf" label="Teléfono" hint="Introduzca su telefono" placeholder="6xx xxx xxx" />
            </div>
            <div class="col-0 col-sm-0 col-md-2 col-lg-2"></div>
            <div class="col-12 col-sm-12 col-md-5 col-lg-5">
                <q-select outlined v-model="razon" :options="options" label="Razón" hint="Seleccione una razón" />
            </div>
        </div>
        <div class="row rowInputs">
            <div class="col-12 col-sm-12 col-md-12 col-lg-12">
            <q-input outlined v-model="mensaje" label="Mensaje" hint="Introduzca su texto" placeholder="Mensaje" autogrow/>
            </div>
        </div>
           <div class="row rowButtons">
            <div class="col-12 col-sm-12 col-md-12 col-lg-12">
                <q-btn color="negative" label="Cancelar" @click="aviso" />
                <q-btn color="positive" label="Enviar" @click="enviar"/>
            </div>
        </div>
    </q-page>
</template>

<script>
export default {
  name: 'contacto',
  data () {
    return {
      email: null,
      nombre: null,
      telefono: null,
      razon: null,
      options: [
        'Soy pc master race', 'Soy piknin', 'Soy sonyer', 'Soy xboxer'
      ]
    }
  },
  methods: {
    aviso () {
      var numero1 = 1
      var numero2 = 2
      if (numero1 < numero2) {
        this.$q.notify({
          message: 'Error en el forulario',
          color: 'red',
          position: 'top-right',
          icon: 'announcement'
        })
      }
    },
    enviar () {
      this.$q.notify({
        message: 'Correo Enviado',
        color: 'red',
        position: 'top-right',
        icon: 'announcement'
      })
    }
  }
}

</script>
