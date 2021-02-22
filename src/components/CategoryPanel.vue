<template>
  <v-container>
    <v-row>
      <v-col align="center" class="ml-2">
        <v-img :style="wildCard" src="../assets/select01.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isCategoryUsed0 }"
          ></div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img :style="wildCard" src="../assets/select02.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isCategoryUsed1 }"
          ></div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img :style="wildCard" src="../assets/select03.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isCategoryUsed2 }"
          ></div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img :style="wildCard" src="../assets/select04.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isCategoryUsed3 }"
          ></div>
        </v-img>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "CategoryPanel.vue",
  props: {
    isCategoryUsed0: {
      type: Boolean,
      required: true
    },
    isCategoryUsed1: {
      type: Boolean,
      required: true
    },
    isCategoryUsed2: {
      type: Boolean,
      required: true
    },
    isCategoryUsed3: {
      type: Boolean,
      required: true
    },
    elementWidth: {
      type: Number,
      required: true
    }
  },
  computed: {
    wildCard: function() {
      return {
        width: this.elementWidth + "px"
      };
    }
  }
};
</script>

<style scoped>
.repeating-gradient {
  background-image: url("../assets/red-x-transparent.png");
  background-position: center center;
  background-size: contain;
}
</style>
