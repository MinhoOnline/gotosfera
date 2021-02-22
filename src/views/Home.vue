<template>
  <v-container fluid class="ma-0 pa-0">
    <questions />
  </v-container>
</template>

<script>
// @ is an alias to /src
import Questions from "@/components/Questions.vue";

export default {
  name: "Home",
  components: {
    Questions
  }
};
</script>

<style></style>
