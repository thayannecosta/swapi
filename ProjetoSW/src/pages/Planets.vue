<template>
  <q-page padding>
    <div class="q-pa-md text-h3 text-center" style="padding-bottom:25px">
      <div class="row items-start q-gutter-md">
        <q-toolbar class="text-dark">
        <q-btn flat round icon="west" to="/" />
        </q-toolbar>
        </div>
    </div>
      <div class="text-h3 text-center" style="padding-bottom: 25px">Planetas</div>
        <div class="row justify-center">
          <div class="col-12 col-md-8" style="margin-left: 15px;">
              <q-input type="search"
                style="padding-bottom: 25px"
                v-model="buscaPlaneta"
                debounce="500"
                filled
                @keyup="fazerPesquisaPlaneta"
                placeholder="Pesquisa"
              >
              <template v-slot:append>
                <q-icon @click="fazerPesquisaPlaneta" color="primary" name="search" />
              </template>
              </q-input>
      </div>
    </div>
    <div class="row items-start col-12 q-col-gutter-md">
      <div v-for="planet in planets" :key="planet.name" class="col-12 col-sm-6 col-md-4 col-lg-3">
        <q-card flat bordered>

            <q-item-section items-start>
              <q-item-label overline>{{planet.name}}</q-item-label>
                <q-item-label caption>
                Population:   {{planet.population}}
                </q-item-label>
            </q-item-section>

          <q-separator />

          <q-card-section>
            <q-card-section>
              Climate: {{planet.climate}}
            </q-card-section>
            <q-card-section>
              Terrain: {{planet.terrain}}
            </q-card-section>

            <q-separator vertical />
            <q-card-section class="col-4">
            Diameter: {{planet.diameter}}
            </q-card-section>
            <q-card-section class="col-4">
            Rotation Period: {{planet.rotation_period}}
            </q-card-section>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Planets',
  data () {
    return {
      planets: {},
      buscaPlaneta: ''
    }
  },
  methods: {
    fazerPesquisaPlaneta () {
      const urlPlaneta = 'https://swapi.dev/api/planets/?search=' + this.buscaPlaneta
      this.$axios.get(urlPlaneta)
        .then(response => {
          this.planets = response.data.results
        })
    }
  },
  beforeMount () {
    this.fazerPesquisaPlaneta()
  }
}
</script>
