<template>
  <q-page padding>
    <div class="text-h3 text-center">Personagens</div>
    <q-item clickable v-ripple v-for="name in people" :key="name.people">
        <q-item-section>
          <q-item-label overline>{{people.name}}</q-item-label>
          <q-item-label>{{people.birth_year}}</q-item-label>
        </q-item-section>
        <q-item-section thumbnail>
          <img src="">
        </q-item-section>
      </q-item>
  </q-page>
</template>

// v-for="people in people" :key="people.name"> {{people.name}}
<script>
export default {
  name: 'People',
  data () {
    return {
      people: {}

    }
  },
  methods: {
    listarPersonagens () {
      this.$axios.get('https://swapi.dev/api/people/1')
        .then(response => {
          this.people = (response.data)
        })
    }
  },
  beforeMount () {
    this.listarPersonagens()
  }
}
</script>
