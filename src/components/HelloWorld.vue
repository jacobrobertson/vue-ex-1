<template>

  <v-container>


    <v-row>
      <Traits id="traits1"></Traits>
    </v-row>

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

    <v-container v-if="selectedsummoner.name">
    <v-row>
      <v-col>
        <v-card class="mx-auto">
          <v-toolbar>
            <v-toolbar-title class="grey--text">{{ selectedsummoner.name }} played against X players including these in their last 10 games...</v-toolbar-title>
            <v-spacer></v-spacer>

            <v-tooltip top max-width="50em">
              <template v-slot:activator="{ on }">
                <v-btn icon v-on="on">
                  <v-icon color="grey lighten-1">mdi-information</v-icon>
                </v-btn>
              </template>
              <span>{{ selectedsummoner.name }} was matched against X players including these in the last X games, 
                which means they are the types of players that {{ selectedsummoner.name }}
                will be matched against in upcoming games.</span>
            </v-tooltip>
          </v-toolbar>

          <Faces id="abc2" :facerows="1" :facecols="8" facesize="60" />
          <v-card-text style="height: 150px;">
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
            <v-toolbar-title class="grey--text">...and those X players played against X other players including these in their last X games.</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-tooltip top max-width="50em">
              <template v-slot:activator="{ on }">
                <v-btn icon v-on="on">
                  <v-icon color="grey lighten-1">mdi-information</v-icon>
                </v-btn>
              </template>
              <span>{{ selectedsummoner.name }} might not have played against these players, but they're the types
                of players they're likely to be matched up against in upcoming games.
              </span>
            </v-tooltip>
          </v-toolbar>

          <Faces id="abc1" :facerows="2" :facecols="16" facesize="25" />
          <v-card-text style="height: 135px;">
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
  </v-container>
</template>

<script>
  import Faces from './Faces.vue'
  import Traits from './Traits.vue'
  export default {
    name: 'HelloWorld',
    components: {
      Faces, Traits
    },
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
        /*
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
'corper s',
'it amet justo Se',
'd ultrices tempo',
'r odio a posuere',
'Etiam ac posuere q',
'uam vitae ullamcor',
'per ligula',
'Phasellus ut m',
'assa lacinia sce',
'lerisque mas',
'sa vitae',
'aliquam',
'risus Duis blandit',
'purus sit',
'amet te',
'llus volutpat l',
'acinia Praesent sce',
'lerisque p',
'urus vitae',
'lorem finib',
'us non mattis purus',
'venenatis Aliq',
'uam ac ex',
'sit amet',
'enim cursus fringill',
'a Sed sed a',
'nte pellen',
'tesque auctor felis',
'non elementum',
'ante Etia',
'm tempus nunc magna',
'eget pel',
*/
'lentesque',
'enim aliquam ut C',
'ras et ege',
'stas arcu',
'in aliquam veli',
't Donec fini',
'bus velit port',
'titor fringilla pla',
      ],
      theirsummoners: [
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
/*
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
'vitae commodo lectus',
'Maecenas vel',
'nunc nunc',
'Nullam sapie',
'n felis vestibul',
'um sed co',
'nvallis a cur',
'sus quis m',
'assa Sed in',
'velit d',
'ui Morbi',
'gravida lobortis maxi',
'mus Nullam condiment',
'um enim sit amet vel',
'it ultricies',
'non lacinia nunc v',
'ehicula Viv',
'amus bibend',
'um nec quam id eg',
'estas Suspend',
'isse et scelerisque',
'tellus Integer cons',
'equat dict',
'um massa',
'eget plac',
'erat erat Etiam',
'posuere in felis soda',
'les mollis',
'Proin blandit',
'erat sed ex pla',
'cerat rhoncu',
's Nullam a elit',
'ut odio sod',
'ales lobor',
'tis at vel d',
'uiIn rutru',
'm pharetra vi',
'verra Sed da',
'pibus ris',
'us eget eros viverra',
'interdum Donec pr',
'etium ipsum p',
'orta dapibus justo',
'non pos',
'uere neque Donec',
'ut lorem',
'sit amet tortor s',
'celerisque varius ac',
'ut metus Dui',
's maximu',
's nulla at nibh phare',
'tra molestie',
'Cras hend',
'rerit lor',
'em orci quis eleifen',
'd sapien',
'ultricies in Sus',
'pendisse viverra n',
'isi in imperdiet sus',
'cipit Curab',
'itur tempus dolo',
'r vel ph',
'aretra pretium lacu',
's lacus consequat v',
'elit et pretium ni',
'si felis at s',
'apien Fusce',
'et bibendum le',
'ctus Nul',
'la consequat',
'scelerisque alique',
't Mauris',
'non felis sit',
'amet sapien grav',
'ida pulvinarMauri',
's rutrum nun',
'c quis risus finibus',
'tempor Cras',
'lobortis',
'id libero eg',
'et lacinia Vivamus p',
'ulvinar ex nib',
'h fringil',
'la maximus a',
'ugue dapibus quis',
'Maecenas pulvina',
'r mauris quis',
'maximus sodales',
'felis lorem digniss',
'im augue',
'in sollicit',
'udin eros',
'lorem in n',
'isl Vivam',
'us condiment',
'um augue libero nec',
'faucibus lacus tem',
'por a P',
'ellentes',
'que pharetra diam id',
'ipsum rhoncus ac te',
'mpor massa',
'pellentesque Quisq',
'ue dictum eu nisi e',
'get euismod Proin a',
'liquet sod',
'ales lobortis Qu',
'isque vel nun',
'c vehicula a',
'liquam ipsum vel',
'imperdiet sem Ut',
'lacinia',
'orci vel temp',
'or tincidunt risu',
*/
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
