<template>
  <q-page padding>
    <q-btn-dropdown class="" style="margin-bottom: 20px" color="primary" label="Mudar Página">
      <q-list>
        <q-item clickable v-close-popup @click="onItemClick">
          <q-item-section>
            <q-item-label>Planetas</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-btn-dropdown>
      <div class="text-h3 text-center" style="padding-bottom: 25px">Personagens</div>
        <div class="row justify-center">
          <div class="col-12 col-md-8" style="margin-left: 15px;">
              <q-input type="search"
                style="padding-bottom: 25px"
                v-model="buscaNome"
                debounce="500"
                filled
                @keyup="fazerPesquisa"
                placeholder="Pesquisa"
              >
              <template v-slot:append>
                <q-icon @click="fazerPesquisa" color="primary" name="search" />
              </template>
              </q-input>
          </div>
        </div>
    <div class="row items-start col-12 q-col-gutter-md">
      <div v-for="person in people" :key="person.name" class="col-12 col-sm-6 col-md-4 col-lg-3">
        <q-card flat bordered>

            <q-item-section items-start>
              <q-item-label overline>{{person.name}}</q-item-label>
                <q-item-label caption>
                Birth Year:   {{person.birth_year}}
                </q-item-label>
            </q-item-section>

          <q-separator />

          <q-card-section>
            <q-card-section>
              Gender: {{person.gender}}
            </q-card-section>
            <q-card-section>
              Skin Color: {{person.skin_color}}
            </q-card-section>

            <q-separator vertical />
            <q-card-section class="col-4">
            Mass: {{person.mass}}
            </q-card-section>
            <q-card-section class="col-4">
            Height: {{person.height}}
            </q-card-section>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'People',
  data () {
    return {
      people: {},
      buscaNome: ''
    }
  },
  methods: {
    // listarPersonagens () {
    //   this.$axios.get('https://swapi.dev/api/people')
    //     .then(response => {
    //       this.people = response.data.results
    //     })
    // },
    fazerPesquisa () {
      const url = 'https://swapi.dev/api/people/?search=' + this.buscaNome
      this.$axios.get(url)
        .then(response => {
          this.people = response.data.results
        })
    },
    onItemClick () {
      this.$router.push('/Planets')
    }
  },
  beforeMount () {
    this.fazerPesquisa()
  }
}
</script>
