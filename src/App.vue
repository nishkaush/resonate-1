<template>
  <v-app>
    <h1 class="text-xs-center pa-5">ThreeTale</h1>
    <v-container>
      <v-layout class="mt-5" v-if="!showOptionsScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <h2>Rate Your Experience</h2>
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

      <v-layout v-if="showOptionsScreen">
        <v-flex class="text-xs-center" xs12 md8 offset-md2>
          <h1>Hi I am screen for choosing options</h1>
          <h3>Your chosen rating is {{chosenRating}}</h3>
          <p>{{goodOrBadText}}</p>
          <v-icon x-large v-for="(n,i) in 5" :key="i" class="star pt-3">star</v-icon>
          <div class="d-flex">
            <p v-for="item in optionsArr" :key="item">{{item}}</p>
          </div>
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
    chooseRating(chosenIndex) {
      this.chosenRating = chosenIndex + 1;
      this.showOptionsScreen = true;
      this.chosenRating > 3
        ? (this.goodOrBadText = "What went well")
        : (this.goodOrBadText = "What could be Improved");
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
</style>
