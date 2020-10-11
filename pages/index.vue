<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card
        v-for="food in foods"
        :key="food.id"
        elevation="2"
        outlined
        shaped
      >
        {{ food.name }}
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import gql from 'graphql-tag'
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  apollo: {
    foods: gql`query{
      foods{
        id
        name
        calories
        description
        date
      }
    }`
  },
  methods: {
    addFood () {
      this.$apollo.mutate({
        mutation: gql`
          mutation($id: ID, $name: String, $calories: Int, $description: String, $date: String ){
            addFood(id: $id, name: $name, calories: $calories, description: $description, date: $date){
              name
            }
          }
        `,
        variables: {

        }
      })
    }
  }
}
</script>
