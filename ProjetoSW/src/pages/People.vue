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
          <div class="col-md-6" style="margin-left: 15px;">
              <q-input
                style="padding-bottom: 25px"
                v-model="buscaNome"
                debounce="500"
                filled
                placeholder="Pesquisa"
              >
              <template v-slot:append>
                <q-icon @click="fazerPesquisa" label="buscaNome" color="primary" name="search" />
              </template>
              </q-input>
              <q-item clickable v-ripple>
                  <q-item-section>
                    <q-item-label overline>{{buscaNome}}</q-item-label>
                    <q-item-label>{{buscaNome}}</q-item-label>
                  </q-item-section>
                </q-item>
          </div>
        </div>

      <div class="q-pa-md row items-start q-gutter-md"
      v-for="person in people" :key="person.name">
      <q-card flat bordered>
      <q-item>
        <q-item-section>
          {{person.date_birth}}
        </q-item-section>

        <q-item-section class="text-left">
          <q-item-label overline>{{person.name}}</q-item-label>
          <q-item-label caption>
           Birth Year:   {{person.birth_year}}
          </q-item-label>
        </q-item-section>
      </q-item>

      <q-separator />

      <q-card-section>
        <q-card-section>
          Gender: {{person.gender}}
        </q-card-section>

        <q-separator vertical />

        <q-card-section class="col-4">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        </q-card-section>
      </q-card-section>
    </q-card>
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
    listarPersonagens () {
      this.$axios.get('https://swapi.dev/api/people')
        .then(response => {
          this.people = response.data.results
        })
    },
    fazerPesquisa () {
      const url = 'https://swapi.dev/api/people/?search=' + this.buscaNome
      this.$axios.get(url)
        .then(response => {
          this.buscaNome = response.data.results
        })
    },
    onItemClick () {
      this.$router.push('/Planets')
    }
  },
  beforeMount () {
    this.listarPersonagens()
  }
}
</script>
