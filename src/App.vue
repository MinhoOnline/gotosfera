<template>
  <v-app style="font-family: 'HearthStone';">
    <v-container fluid class="ma-0 pa-0">
      <v-card class="iframe-container">
        <iframe src="../assets/portada.jpg"></iframe>
        <v-overlay
          class="align-end justify-center d-block"
          style="width: 1900px"
          opacity="0"
          :absolute="true"
          :value="true"
        >
          <router-view />
        </v-overlay>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  })
};
</script>

<style>
.iframe-container {
  overflow: hidden;
  /* 16:9 aspect ratio */
  padding-top: 56.25%;
  position: relative;
}

.iframe-container iframe {
  border: 0;
  height: 100%;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
@font-face {
  font-family: "HearthStone";
  src: url("./assets/BELWEB.TTF") format("truetype");
}
</style>
