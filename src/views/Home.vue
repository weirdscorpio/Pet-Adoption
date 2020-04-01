<template>
  <div class="home-view-container">
    <h1>A new friend for Adoption</h1>
    {{ animalsCount }}
    {{ getAllCats.length }}
    <button class="btn btn-primary" @click="togglePetForm">Add new pet</button>

        <b-form @submit.prevent="handleSubmit"  v-if="showPetForm">

          <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
            <b-form-input
              id="input-2"
              v-model="form.name"
              required
              placeholder="Enter name"
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-3" label="Species:" label-for="input-3">
            <b-form-select
              id="input-3"
              v-model="form.species"
              :options="['cats', 'dogs']"
              required
            ></b-form-select>
          </b-form-group>

          <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
            <b-form-input
              id="input-2"
              v-model="form.age"
              required
              placeholder="Enter name"
            ></b-form-input>
          </b-form-group>

          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
// @ is an alias to /src
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      form: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.form
      var payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      this.form = {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  }
}
</script>
