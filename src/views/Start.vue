<template>
  <v-container>
    <v-row align="center" justify="center" style="margin-top: 700px">
      <v-col align="center">
        <v-img
          src="../assets/piedra.png"
          style="width: 780px; font-size: 90px; color: rgba(25, 25, 25, 100); align-items: center;"
        >
          <div style="margin-top: -24px">
            GRAN FINAL
          </div>
        </v-img>
      </v-col>
    </v-row>
    <v-row justify="center" align="center" style="margin-top: 120px">
      <v-col align="center">
        <v-btn color="green" @click="start()">
          Start
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Start",
  methods: {
    start() {
      this.$router.push("questions");
    }
  }
};
</script>

<style></style>
