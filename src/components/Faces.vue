<template>
  <v-container>
    <v-row v-for="r in facerows" :key="r">
      <v-col v-for="c in facecols" :key="c">
        <v-img 
			:src="randomface(faceicons)" 
			:width="facesize"></v-img>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Faces",
  props: {
		facerows: Number, 
		facecols: Number,
		facesize: Number,
  },
  data: () => ({
	testicon: "../assets/faces/boy-smiling.png",
    faceicons: [
      "amazed-man.png",
      "angry-man.png",
      "angry-woman.png",
      "baby-crying.png",
      "baby-love.png",
      "boy-broad-smile.png",
      "boy-happy-smile.png",
      "boy-smiling.png",
      "boy-suffering.png",
      "delighted-granny.png",
      "disappointed-boy.png",
      "embarrased-boy.png",
      "embarrased-girl.png",
      "embarrased-granny.png",
      "emotive-granny.png",
      "fat-boy-angry.png",
      "fat-boy-shocked.png",
      "fat-boy-smiling.png",
      "fat-boy-sorry.png",
      "fat-boy.png",
      "frightened-hipster.png",
      "girl-air-kissing.png",
      "girl-crying.png",
      "girl-embarrased.png",
      "girl-laughing-to-tears.png",
      "girl-showing-tongue.png",
      "girl-smiling.png",
      "girl-with-poker-face.png",
      "happy-baby.png",
      "happy-woman.png",
      "hipster-smiling.png",
      "hypnotized-hipster.png",
      "inexpressive-girl.png",
      "kissing-girl.png",
      "man-with-moustache-smiling.png",
      "naughty-girl.png",
      "perplexed-man.png",
      "philosophizing-boy.png",
      "sad-baby.png",
      "sad-girl.png",
      "sad-hipster.png",
      "sad-woman.png",
      "satisfied-woman.png",
      "shocked-girl.png",
      "sleeping-granny.png",
      "sleepy-boy.png",
      "smiling-baby.png",
      "smiling-girl.png",
      "surprised-girl.png",
      "suspicious-man.png",
      "teasing-boy.png",
      "upset-girl.png",
      "upset-granny.png",
      "winking-boy.png",
      "wondered-hipster.png"
	],
	randomface: function(faceicons) {
		var index = Math.floor(Math.random() * (faceicons.length - 1));
		return require("../assets/faces/" + faceicons[index]); 
	},
  })
};
</script>