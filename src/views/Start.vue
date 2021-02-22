<template>
  <v-container>
    <v-row style="margin-top: 500px">
      <category-panel
        :elementWidth="360"
        :is-category-used0="isCategoryUsed0"
        :is-category-used1="isCategoryUsed1"
        :is-category-used2="isCategoryUsed2"
        :is-category-used3="isCategoryUsed3"
      />
    </v-row>
    <v-row justify="center" align="center" style="margin-top: 60px">
      <v-col align="center">
        <v-btn color="green" @click="start()">
          Start
        </v-btn>
      </v-col>
      <category-button-panel v-on:CategoryChange="CategoryChange" />
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /src
import CategoryPanel from "@/components/CategoryPanel.vue";
import CategoryButtonPanel from "@/components/CategoryButtonPanel";

export default {
  name: "Start",
  components: {
    CategoryButtonPanel,
    CategoryPanel
  },
  data() {
    return {
      isCategoryUsed0: false,
      isCategoryUsed1: false,
      isCategoryUsed2: false,
      isCategoryUsed3: false
    };
  },
  methods: {
    CategoryChange(index, newValue) {
      switch (index) {
        case 0:
          this.isCategoryUsed0 = newValue;
          break;
        case 1:
          this.isCategoryUsed1 = newValue;
          break;
        case 2:
          this.isCategoryUsed2 = newValue;
          break;
        case 3:
          this.isCategoryUsed3 = newValue;
          break;
      }
    },
    start() {
      this.$router.push("questions");
    }
  }
};
</script>

<style></style>
