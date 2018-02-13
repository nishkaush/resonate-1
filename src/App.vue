<template>
  <v-app>
    <h1 class="text-xs-center pa-5">ThreeTale</h1>
    <v-container>
      <v-layout class="mt-5" v-if="!showOptionsScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <h1 class="blue--text">Please rate your recent experience with us</h1>
          <v-divider class="my-3"></v-divider>
          <v-icon 
          x-large
          v-for="(n,i) in 5" 
          :key="i" 
          class="star pt-3"
          :data-index="i"
          @mouseover="changeStarColors(i)"
          @mouseleave="removeStarColors"
          @click="chooseRating(i)"
          >star</v-icon>
        </v-flex>
      </v-layout>

      <v-layout v-if="showOptionsScreen && !showCommentsScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <v-icon 
          x-large v-for="(n,i) in 5" :key="i" class="star pt-0 mb-5" 
          :color="chosenRating>i?'blue':'gray'"
          >star</v-icon>
          <h2 class="mb-5">{{goodOrBadText}}</h2>
          <div class="mt-3">
            <v-btn 
            round
            v-for="(item,i) in optionsArr" 
            :key="item" class="mx-2 options"
            @click="makeBtnBlue(i)"
            :data-index="i"
            >{{item}}</v-btn>
          </div>
          <v-btn class="mt-5 blue white--text" @click="showCommentsScreen=true">Done</v-btn>
        </v-flex>
      </v-layout>

      <v-layout v-if="showCommentsScreen && !showSuccessScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <div>
            <v-icon 
            x-large v-for="(n,i) in 5" :key="i" class="star pt-0 mb-5" 
            :color="chosenRating>i?'blue':'gray'"
            >star</v-icon>
          </div>
          <v-btn>Availability</v-btn>
          <v-btn>Opening Hours</v-btn>
          <h2 class="mt-5">Can You Tell us more about your experience</h2>
          <v-text-field textarea label="Type here"></v-text-field>
          <v-btn large class="blue white--text" @click="showSuccessScreen=true">Submit</v-btn>
        </v-flex>
      </v-layout>

      <v-layout v-if="showSuccessScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <v-icon color="green" class="mb-4 mt-3" x-large>check_circle</v-icon>
          <h3>Thanks for taking time to help us understand you better!</h3>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      chosenRating: "",
      showOptionsScreen: false,
      showCommentsScreen: false,
      showSuccessScreen: false,
      goodOrBadText: "",
      optionsArr: [
        "Availability",
        "Staff Friendliness",
        "Information",
        "Loyalty Card",
        "Location",
        "Opening Hours",
        "Solutions",
        "Wait Time"
      ]
    };
  },
  methods: {
    makeBtnBlue(btnIndex) {
      document
        .querySelector(`.options[data-index='${btnIndex}']`)
        .classList.add("options__background");
      document.querySelector(
        `.options[data-index='${btnIndex}']`
      ).style.backgroundColor =
        "blue";
    },
    chooseRating(chosenIndex) {
      this.chosenRating = chosenIndex + 1;
      this.showOptionsScreen = true;
      this.chosenRating > 3
        ? (this.goodOrBadText = "What went well?")
        : (this.goodOrBadText = "What could be Improved?");
    },
    changeStarColors(starIndex) {
      let elementsArr = Array.from(document.querySelectorAll(".star"));
      elementsArr.forEach(e => {
        if (e.dataset.index <= starIndex) {
          return e.classList.add("blueStar");
        }
      });
    },
    removeStarColors() {
      let elementsArr = Array.from(document.querySelectorAll(".star"));
      elementsArr.forEach(e => e.classList.remove("blueStar"));
    }
  }
};
</script>



<style scoped>
.star:hover {
  cursor: pointer;
}
.blueStar {
  color: blue;
}
.options {
  border: 1px solid #939393;
  color: #323232;
}
.options__background {
  background-color: blue;
  color: white;
}
</style>
