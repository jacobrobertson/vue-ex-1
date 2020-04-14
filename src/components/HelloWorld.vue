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
            <v-toolbar-title class="grey--text">{{ selectedsummoner.name }} played against X players like these in the last 10 games...</v-toolbar-title>
            <v-spacer></v-spacer>

            <v-tooltip v-model="show" top max-width="50em">
              <template v-slot:activator="{ on }">
                <v-btn icon v-on="on">
                  <v-icon color="grey lighten-1">mdi-information</v-icon>
                </v-btn>
              </template>
              <span>{{ selectedsummoner.name }} was matched against X players like these in the last X games, 
                which means they are the types of players that {{ selectedsummoner.name }}
                will be matched against in upcoming games.</span>
            </v-tooltip>

          </v-toolbar>
          <v-divider></v-divider>

          <v-card-text style="height: 200px;">
            <vue-word-cloud
                :words="yoursummoners"
                :color="(value) => wordcloudcolor(value)"
                :weight="(value) => wordcloudweight(value)"
                :rotation="(value) => wordcloudrotation(value)"
                font-family="Roboto"
                animation-overlap="5"
                font-size-ratio="1.5"
                rotation-unit="deg"
              />
          </v-card-text>
        </v-card>
      </v-col>
      <v-col>
        <v-card class="mx-auto">
          <v-toolbar>
            <v-toolbar-title class="grey--text">...and those X players played against X other players like these in their last X games.</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon>
              <v-icon>mdi-information</v-icon>
            </v-btn>
          </v-toolbar>
          <v-divider></v-divider>

          <v-card-text style="height: 200px;">
            <vue-word-cloud
                :words="theirsummoners"
                :color="(value) => wordcloudcolor(value)"
                :weight="(value) => wordcloudweight(value)"
                :rotation="(value) => wordcloudrotation(value)"
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
      wordcloudcolor: function (value) {
        if (value.length > 15) {
          return 'grey';
        } else if (value.length > 10) {
          return '#607D8B';
        } else {
          return 'black';
        }
      },
      wordcloudweight: function (value) {
        var len = value.length;
        if (len > 20) {
          len = 20;
        }
        return (5 - (len / 5));
      },
      wordcloudrotation: function (value) {
        return (12 - value.length) * 2;
      },
      yoursummoners: [
        'abcdefg', 'akdj33', 'zzzzabcdefg',
        'isse et scelerisque',
'tellus Integer cons',
'equat dict',
'um massa',
'eget plac',
'erat erat Etiam',
'posuere in felis soda',
'les mollis',
'Proin blandit',
'piscing elit Curabit',
'ur rutrum cursus',
'purus Sed magna ante',
'lacinia a risus nec',
'fermentum luctus di',
'am Pellentesque eg',
'et tristique j',
'usto Integer in',
'tempor arcu',
'Praesent feugiat',
'elit at element',
'um fringilla',
'Cras aliquet aliqu',
'am elit a mo',
'lestie dolor consec',
'tetur quis',
'Aenean te',
'mpor ipsum a ma',
'lesuada',
'accumsan felis nibh',
      ],
      theirsummoners: [
        'sydfsdf-abcdefger', 'akdjf2433', 'zzzzabcdefg',
        'ysdfsdfcdefg', '4akdjfs32433 sd fd', 'z4zzdefg',
        'sdfysdf-abcdefg', '3akdjfs32433', 'zzabcdefg',
        'sdfsy-abcdefg', '1akdj433', 'zzzabdefg',
        'Lorem ips',
'um dolor sit',
'amet consec',
'tetur adi',
'piscing elit Curabit',
'ur rutrum cursus',
'purus Sed magna ante',
'lacinia a risus nec',
'fermentum luctus di',
'am Pellentesque eg',
'et tristique j',
'usto Integer in',
'tempor arcu',
'Praesent feugiat',
'elit at element',
'um fringilla',
'Cras aliquet aliqu',
'am elit a mo',
'lestie dolor consec',
'tetur quis',
'Aenean te',
'mpor ipsum a ma',
'lesuada',
'accumsan felis nibh',
'tempor ma',
'gna eget',
'commodo ma',
'uris odio in',
'mauris Vestibulum f',
'elis quam',
'luctus non magna v',
'el pellentesque',
'blandit',
'tellus Prae',
'sent et orci et null',
'a iaculis tristi',
'que Vestibulum in s',
'emper velit i',
'n semper diam',
'Fusce tortor sem',
'venenatis eu dictum',
'eu posuere v',
'olutpat magna F',
'usce dict',
'um diam vel null',
'a semper molesti',
'e Morbi ut dui',
'orci Nu',
'lla facilisi Nunc',
'dui elit',
'interdum id tempus la',
'oreet ves',
'tibulum sceler',
'isque nisi Aliquam',
'elementum commod',
'o nisl et commodo',
'Vivamus v',
'ulputate',
'non urna sit ame',


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
