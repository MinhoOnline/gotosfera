<template>
  <v-row align="center">
    <v-col class="ml-8 mr-n10">
      <v-btn
        :color="isAnswerMarked0 ? 'light-gray' : getColor()"
        @click="click(0)"
        class="mr-4"
      >
        A
      </v-btn>
    </v-col>

    <v-col class="ml-n10 mr-n10">
      <v-btn
        :color="isAnswerMarked1 ? 'light-gray' : getColor()"
        @click="click(1)"
        class="mr-4"
      >
        B
      </v-btn>
    </v-col>
    <v-col class="ml-n10 mr-n10">
      <v-btn
        :color="isAnswerMarked2 ? 'light-gray' : getColor()"
        @click="click(2)"
        class="mr-4"
      >
        C
      </v-btn>
    </v-col>
    <v-col class="ml-n10 mr-n10">
      <v-btn
        :color="isAnswerMarked3 ? 'light-gray' : getColor()"
        @click="click(3)"
        class="mr-4"
      >
        D
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "AnswerButtonPanel",
  props: {
    buttonColor: {
      type: String,
      required: true
    }
  },
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
    },
    getColor() {
      switch (this.buttonColor) {
        case "red":
          return "red darken-1";
        case "yellow":
          return "yellow darken-1";
      }
    }
  }
};
</script>

<style scoped></style>
