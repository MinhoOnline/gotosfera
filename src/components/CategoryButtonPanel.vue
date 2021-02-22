<template>
  <v-col align="center">
    <v-btn
      :color="!isMarked0 ? 'light-green' : 'red darken4'"
      @click="click(0)"
      class="mr-4"
      fab
    >
      <v-icon>
        mdi-bookmark-outline
      </v-icon>
    </v-btn>
    <v-btn
      :color="!isMarked1 ? 'light-green' : 'red darken4'"
      @click="click(1)"
      class="mr-4"
      fab
    >
      <v-icon>
        mdi-bookmark-outline
      </v-icon>
    </v-btn>
    <v-btn
      :color="!isMarked2 ? 'light-green' : 'red darken4'"
      @click="click(2)"
      class="mr-4"
      fab
    >
      <v-icon>
        mdi-bookmark-outline
      </v-icon>
    </v-btn>
    <v-btn
      :color="!isMarked3 ? 'light-green' : 'red darken4'"
      @click="click(3)"
      class="mr-4"
      fab
    >
      <v-icon>
        mdi-bookmark-outline
      </v-icon>
    </v-btn>
  </v-col>
</template>

<script>
export default {
  name: "CategoryButtonPanel",
  data() {
    return {
      isMarked0: false,
      isMarked1: false,
      isMarked2: false,
      isMarked3: false
    };
  },
  methods: {
    click(index) {
      switch (index) {
        case 0:
          this.isMarked0 = !this.isMarked0;
          this.$emit("CategoryChange", index, this.isMarked0);
          break;
        case 1:
          this.isMarked1 = !this.isMarked1;
          this.$emit("CategoryChange", index, this.isMarked1);
          break;
        case 2:
          this.isMarked2 = !this.isMarked2;
          this.$emit("CategoryChange", index, this.isMarked2);
          break;
        case 3:
          this.isMarked3 = !this.isMarked3;
          this.$emit("CategoryChange", index, this.isMarked3);
          break;
      }
    }
  }
};
</script>

<style scoped></style>
