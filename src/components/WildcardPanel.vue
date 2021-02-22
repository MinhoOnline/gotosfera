<template>
  <v-container>
    <v-row class="mt-4">
      <v-col cols="4" align="center"> </v-col>
      <v-col align="center" class="ml-2">
        <v-img class="wildcard" src="../assets/wildcard01.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed0 }"
          >
            <v-icon color="white" size="60" style="margin-top: 185px">
              mdi-help-circle
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img class="wildcard" src="../assets/wildcard02.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed1 }"
          >
            <v-icon color="white" size="60" style="margin-top: 185px">
              mdi-percent
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col cols="4" align="center"> </v-col>
    </v-row>
    <v-row class="mt-n4">
      <v-col cols="4" align="center"> </v-col>
      <v-col align="center">
        <v-img class="wildcard" src="../assets/wildcard03.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed2 }"
          >
            <v-icon color="white" size="60" style="margin-top: 185px">
              mdi-forum
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img
          v-if="!allWildcards"
          class="wildcard"
          src="../assets/cardback.png"
        ></v-img>
        <v-img
          v-if="allWildcards"
          class="wildcard"
          src="../assets/wildcard04.png"
        >
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed3 }"
          >
            <v-icon color="white" size="60" style="margin-top: 185px">
              mdi-restart
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col cols="4" align="center"> </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "WildcardPanel.vue",
  props: {
    isWildcardUsed0: {
      type: Boolean,
      required: true
    },
    isWildcardUsed1: {
      type: Boolean,
      required: true
    },
    isWildcardUsed2: {
      type: Boolean,
      required: true
    },
    isWildcardUsed3: {
      type: Boolean,
      required: true
    },
    allWildcards: {
      type: Boolean,
      default: false,
      required: false
    }
  },
  data() {
    return {};
  }
};
</script>

<style scoped>
.wildcard {
  width: 200px;
}
.repeating-gradient {
  background-image: url("../assets/red-x-transparent.png");
  background-position: center center;
  background-size: contain;
}
</style>
