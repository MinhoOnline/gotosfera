<template>
  <v-container>
    <v-row class="mt-4">
      <v-col align="center"> </v-col>
      <v-col align="center">
        <v-img class="wildcard" src="../assets/wildcard01.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed0 }"
          >
            <v-icon color="white" size="30" style="margin-top: 92px">
              mdi-help-circle
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img class="wildcard" src="../assets/wildcard05.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed1 }"
          >
            <v-icon color="white" size="30" style="margin-top: 92px">
              mdi-forum
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col align="center">
        <v-img class="wildcard" src="../assets/wildcard04.png">
          <div
            class="fill-height"
            v-bind:class="{ 'repeating-gradient': isWildcardUsed2 }"
          >
            <v-icon color="white" size="30" style="margin-top: 92px">
              mdi-restart
            </v-icon>
          </div>
        </v-img>
      </v-col>
      <v-col align="center"> </v-col>
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
    }
  },
  data() {
    return {};
  }
};
</script>

<style scoped>
.wildcard {
  width: 100px;
}
.repeating-gradient {
  background-image: url("../assets/red-x-transparent.png");
  background-position: center center;
  background-size: contain;
}
</style>
