<template>
  <v-col align="center">
    <v-btn
      :color="!isAnswerMarked0 ? 'light-green' : 'red darken4'"
      @click="click(0)"
      class="mr-4"
    >
      A
    </v-btn>
    <v-btn
      :color="!isAnswerMarked1 ? 'light-green' : 'red darken4'"
      @click="click(1)"
      class="mr-4"
    >
      B
    </v-btn>
    <v-btn
      :color="!isAnswerMarked2 ? 'light-green' : 'red darken4'"
      @click="click(2)"
      class="mr-4"
    >
      C
    </v-btn>
    <v-btn
      :color="!isAnswerMarked3 ? 'light-green' : 'red darken4'"
      @click="click(3)"
      class="mr-4"
    >
      D
    </v-btn>
  </v-col>
</template>

<script>
export default {
  name: "AnswerButtonPanel",
  data() {
    return {
      isAnswerMarked0: false,
      isAnswerMarked1: false,
      isAnswerMarked2: false,
      isAnswerMarked3: false
    };
  },
  methods: {
    click(index) {
      switch (index) {
        case 0:
          this.isAnswerMarked0 = !this.isAnswerMarked0;
          this.$emit("AnswerChange", index, this.isAnswerMarked0);
          break;
        case 1:
          this.isAnswerMarked1 = !this.isAnswerMarked1;
          this.$emit("AnswerChange", index, this.isAnswerMarked1);
          break;
        case 2:
          this.isAnswerMarked2 = !this.isAnswerMarked2;
          this.$emit("AnswerChange", index, this.isAnswerMarked2);
          break;
        case 3:
          this.isAnswerMarked3 = !this.isAnswerMarked3;
          this.$emit("AnswerChange", index, this.isAnswerMarked3);
          break;
      }
    }
  }
};
</script>

<style scoped></style>
