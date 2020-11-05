<template>
  <q-page class="q-pa-md">
    <div class="row">
            <div class="col-12">
                <div class="q-pa-md q-gutter-sm">
                 <q-breadcrumbs>
                    <q-breadcrumbs-el icon="home" to="/" />
                    <q-breadcrumbs-el :label="Info" icon="info" />
                </q-breadcrumbs>
              </div>
            </div>
    </div>
    <div class="row rowTitle">
        <div class="col-12">
            <h3>Información</h3>
        </div>
    </div>
    <div class="row">
        <div class="col-12">
            <p class="textoLorem"><span class="fraseFamosa">CD Projekt Red anunció el martes pasado un nuevo retraso de Cyberpunk 2077 que pospondría el esperado juego de rol futurista hasta el 10 de diciembre de 2020.</span> En el comunicado oficial apuntaban que los 21 días de tiempo extra los utilizarían para pulir el parche "Día 0" que saldrá a la vez que el juego. El medio polaco PAP Business afirma que en una conferencia posterior al anuncio se dijo que el motivo del retraso es la optimización en las consolas de actual generación: PS4 y Xbox One.</p>
        </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'info'
}
</script>
