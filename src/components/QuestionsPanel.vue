<template>
  <v-card
    height="180px"
    style="background-color:rgba(0, 0, 0, 0);
                   box-shadow: 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0);"
  >
    <v-row>
      <v-col>
        <v-sheet
          class="d-flex justify-center"
          :class="getQuestionFontSize()"
          color="indigo darken-4"
        >
          {{ question.text }}
        </v-sheet>
      </v-col>
    </v-row>
    <v-row class="mt-3">
      <v-col>
        <v-sheet
          :color="getColor(0)"
          elevation="18"
          height="80"
          shaped
          width="750"
          class="d-flex align-center ml-4"
          :class="getAnswerFontSize(0)"
        >
          <v-chip class="ma-2" :color="getColor(0)" text-color="white">
            <v-avatar
              left
              :color="getColor(0)"
              style="font-size: 24px;"
              class="mr-4"
            >
              A
            </v-avatar>
          </v-chip>
          {{ question.answers[0] }}
        </v-sheet>
      </v-col>
      <v-spacer />
      <v-col>
        <v-sheet
          :color="getColor(1)"
          elevation="18"
          height="80"
          shaped
          width="750"
          class="d-flex align-center ml-4"
          :class="getAnswerFontSize(1)"
        >
          <v-chip
            class="ma-2"
            :color="getColor(1)"
            text-color="white"
            style="font-size: 32px;"
          >
            <v-avatar
              left
              :color="getColor(1)"
              style="font-size: 24px;"
              class="mr-4"
            >
              B
            </v-avatar>
          </v-chip>
          {{ question.answers[1] }}
        </v-sheet>
      </v-col>
    </v-row>
    <v-row class="mt-3">
      <v-col>
        <v-sheet
          :color="getColor(2)"
          elevation="18"
          height="80"
          shaped
          width="750"
          class="d-flex align-center ml-4"
          :class="getAnswerFontSize(2)"
        >
          <v-chip
            class="ma-2"
            :color="getColor(2)"
            text-color="white"
            style="font-size: 32px;"
          >
            <v-avatar
              left
              :color="getColor(2)"
              style="font-size: 24px;"
              class="mr-4"
            >
              C
            </v-avatar>
          </v-chip>
          {{ question.answers[2] }}
        </v-sheet>
      </v-col>
      <v-spacer />
      <v-col>
        <v-sheet
          :color="getColor(3)"
          elevation="18"
          height="80"
          shaped
          width="750"
          class="d-flex align-center ml-4"
          :class="getAnswerFontSize(3)"
        >
          <v-chip
            class="ma-2"
            :color="getColor(3)"
            text-color="white"
            style="font-size: 32px;"
          >
            <v-avatar
              left
              :color="getColor(3)"
              style="font-size: 24px;"
              class="mr-4"
            >
              D
            </v-avatar>
          </v-chip>
          {{ question.answers[3] }}
        </v-sheet>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: "QuestionsPanel",
  props: {
    question: {
      type: Object,
      required: true
    },
    isP1AnswerMarked0: {
      type: Boolean,
      required: true
    },
    isP1AnswerMarked1: {
      type: Boolean,
      required: true
    },
    isP1AnswerMarked2: {
      type: Boolean,
      required: true
    },
    isP1AnswerMarked3: {
      type: Boolean,
      required: true
    },
    isP2AnswerMarked0: {
      type: Boolean,
      required: true
    },
    isP2AnswerMarked1: {
      type: Boolean,
      required: true
    },
    isP2AnswerMarked2: {
      type: Boolean,
      required: true
    },
    isP2AnswerMarked3: {
      type: Boolean,
      required: true
    },
    isCorrectAnswerMarked: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {};
  },
  created() {},
  methods: {
    getQuestionFontSize() {
      if (this.question.text.length > 105) {
        return "question-xl";
      } else if (this.question.text.length > 75) {
        return "question-l";
      } else {
        return "question-m";
      }
    },
    getAnswerFontSize(index) {
      console.log("AFS", this.question.answers[index].length, index);
      if (this.question.answers[index].length > 55) {
        return "answer-xl";
      } else if (this.question.answers[index].length > 45) {
        return "answer-l";
      } else if (this.question.answers[index].length > 10) {
        return "answer-m";
      } else {
        return "answer-s";
      }
    },
    getColor(index) {
      if (this.isCorrectAnswerMarked && this.question.correct === index) {
        return "green darken-1";
      } else {
        switch (index) {
          case 0:
            if (this.isP1AnswerMarked0) {
              if (this.isP2AnswerMarked0) return "orange darken-3";
              else return "red darken-2";
            } else {
              if (this.isP2AnswerMarked0) return "yellow darken-2";
              else return "blue darken-2";
            }
          case 1:
            if (this.isP1AnswerMarked1) {
              if (this.isP2AnswerMarked1) return "orange darken-3";
              else return "red darken-2";
            } else {
              if (this.isP2AnswerMarked1) return "yellow darken-2";
              else return "blue darken-2";
            }
          case 2:
            if (this.isP1AnswerMarked2) {
              if (this.isP2AnswerMarked2) return "orange darken-3";
              else return "red darken-2";
            } else {
              if (this.isP2AnswerMarked2) return "yellow darken-2";
              else return "blue darken-2";
            }
          case 3:
            if (this.isP1AnswerMarked3) {
              if (this.isP2AnswerMarked3) return "orange darken-3";
              else return "red darken-2";
            } else {
              if (this.isP2AnswerMarked3) return "yellow darken-2";
              else return "blue darken-2";
            }
        }
      }
    }
  }
};
</script>

<style>
.question-m {
  font-size: 45px;
}
.question-l {
  font-size: 35px;
}
.question-xl {
  font-size: 29px;
}
.answer-s {
  font-size: 35px !important;
}
.answer-m {
  font-size: 33px !important;
}
.answer-l {
  font-size: 27px !important;
}
.answer-xl {
  font-size: 23px !important;
}
</style>
