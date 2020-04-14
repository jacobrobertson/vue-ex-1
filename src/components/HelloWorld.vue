<template>

  <v-container>
    <v-row>
      <v-col>
        <v-select
          v-model="selectedsummoner"
          :items="summoners"
          filled
          label="Select a Summoner"
          return-object
          item-text="name"
        >
        </v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card class="mx-auto">
          <v-toolbar>
            <v-toolbar-title class="grey--text">{{ selectedsummoner.name }} played these X Summoners in the last 10 games...</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon>
              <v-icon>mdi-information</v-icon>
            </v-btn>
          </v-toolbar>
          <v-divider></v-divider>

          <v-card-text style="height: 200px;">
            <vue-word-cloud
                :words="yoursummoners"
                :color="([, weight]) => weight > 10 ? 'DeepPink' : weight > 5 ? 'RoyalBlue' : 'Indigo'"
                font-family="Roboto"
              />
          </v-card-text>
        </v-card>
      </v-col>
      <v-col>
        <v-card class="mx-auto">
          <v-toolbar>
            <v-toolbar-title class="grey--text">...and those X Summoners played these X Summoners in their last 10 games.</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon>
              <v-icon>mdi-information</v-icon>
            </v-btn>
          </v-toolbar>
          <v-divider></v-divider>

          <v-card-text style="height: 200px;">
            <vue-word-cloud
                :words="theirsummoners"
                :color="([value, weight]) => value.substring(0,1) == 'a' ? 'DeepPink' : value.substring(0,1) == 'y' ? 'RoyalBlue' : 'Indigo'"
                :weight="([value, weight]) => value.substring(0,1) == 'a' ? 1 : value.substring(0,1) == 'y' ? 2 : 3"
                :rotation="([value, weight, rotation]) => value.substring(0,1) == 'a' ? 15 : value.substring(0,1) == 'y' ? -15 : 0"
                font-family="Roboto"
                animation-overlap="5"
                font-size-ratio="1.5"
                rotation-unit="deg"
              />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title>
            <v-icon large left>mdi-domain</v-icon>
            <span class="title font-weight-light">Recommendations for {{ selectedsummoner.name }}</span>
          </v-card-title>
          <v-data-table
            :headers="headers"
            :items="selectedsummoner.friends"
            :items-per-page="5"
            class="elevation-1"
            hide-default-footer
          ></v-data-table>
        </v-card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      title: 'hello kitty',
      selectedsummoner: {},
      yoursummoners: [
        ['abcdefg', 1], ['akdjfs32433', 1], ['zzzzabcdefg', 1],
      ],
      theirsummoners: [
        'sydfsdf-abcdefg', 'akdjfs32433', 'zzzzabcdefg',
        'ysdfsdf-abcdefg', '4akdjfs32433', 'z4zzzabcdefg',
        'sdfysdf-abcdefg', '3akdjfs32433', 'zzabcdefg',
        'sdfsdfy-abcdefg', '1akdjfs32433', 'zzzabcdefg',
      ],
      headers: [
        {
          text: 'summoner (100g serving)',
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
      summoners: [
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
