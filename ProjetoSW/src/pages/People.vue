<template>
  <q-page padding>
    <div class="text-h3 text-center">Personagens</div>
    <div class="row">
          <div class="col-md-6" style="margin-left: 15px;">
            <q-input
              v-model="buscaNome"
              debounce="500"
              filled
              placeholder="Pesquisa"
            >
              <template v-slot:string>
                <q-icon @click="fazerPesquisa" name="search" />
              </template>
            </q-input>
          </div>
        </div>
        <q-item-section>{{buscaNome}}</q-item-section>
    <q-item clickable v-ripple v-for="person in people" :key="person.name">
        <q-item-section>
          <q-item-label overline>{{person.name}}</q-item-label>
          <q-item-label>{{person.birth_year}}</q-item-label>
        </q-item-section>
        <q-item-section thumbnail>
          <img src="">
        </q-item-section>
      </q-item>
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
      const url = 'https://swapi.dev/api/people/?search=${this.buscaNome}'
      this.$axios.get(url)
        .then(response => {
          this.buscaNome = response.data.results
        })
    }
  },
  beforeMount () {
    this.listarPersonagens()
  }
}
</script>
