<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="50"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          {{ selecteddessert.iron }} / {{ selecteddessert.name }}
        </h1>

        <v-col class="d-flex" cols="12" sm="6">
          <v-select
            v-model="selecteddessert"
            :items="desserts"
            filled
            label="Select a dessert"
            return-object
            item-text="name"
          >
          </v-select>
        </v-col>

        <template>
          <v-data-table
            :headers="headers"
            :items="selecteddessert.friends"
            :items-per-page="5"
            class="elevation-1"
          ></v-data-table>
        </template>
        
      </v-col>

    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      title: 'hello kitty',
      selecteddessert: {},
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Iron (%)', value: 'iron' },
      ],
      desserts: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%',
          friends: [
            {
              name: 'Ice cream sandwich',
              calories: 237,
              fat: 9.0,
              carbs: 37,
              protein: 4.3,
              iron: '1%',
            },
          ],
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%',
          friends: [
            {
              name: 'Eclair',
              calories: 262,
              fat: 16.0,
              carbs: 23,
              protein: 6.0,
              iron: '7%',
            },
          ],
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%',
          friends: [
            {
              name: 'Eclair',
              calories: 262,
              fat: 16.0,
              carbs: 23,
              protein: 6.0,
              iron: '7%',
            },
            {
              name: 'Eclair Zoo',
              calories: 666,
              fat: 16.0,
              carbs: 23,
              protein: 6.0,
              iron: '10000%',
            },
          ],
        },
      ],
    }),
  }
</script>
