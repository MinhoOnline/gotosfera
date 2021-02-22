<template>
  <v-container fluid>
    <wildcard-panel
      :is-wildcard-used0="isWildcardUsed0"
      :is-wildcard-used1="isWildcardUsed1"
      :is-wildcard-used2="isWildcardUsed2"
      :is-wildcard-used3="isWildcardUsed3"
      :allWildcards="allWildcards"
    />
    <v-stepper
      class="mx-0 px-0"
      alt-labels
      v-model="e1"
      style="background-color:rgba(0, 0, 0, 0);
      box-shadow: 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0);"
    >
      <v-stepper-header class="mb-n5 mt-n5 mx-0 px-0" style="font-size: 18px;">
        <v-row v-for="i in questions.length" :key="i">
          <v-stepper-step
            :complete="e1 > i"
            :step="i"
            color="green darken-1"
            :rules="[() => answers[i - 1]]"
          >
            Pregunta {{ i }}
            <small v-if="i === 5" style="font-size: 14px;">Comodín</small>
            <small v-if="i === 10" style="font-size: 14px;">1 Sub</small>
            <small v-if="i === 13" style="font-size: 14px;">3 Subs</small>
            <small v-if="i === 15" style="font-size: 14px;">5 Subs</small>
          </v-stepper-step>
          <v-divider inset v-if="i !== questions.length"></v-divider>
        </v-row>
      </v-stepper-header>

      <v-stepper-items style="background-color:rgba(0, 0, 0, 0)">
        <v-stepper-content
          step="1"
          style="background-color:rgba(0, 0, 0, 0)"
          :class="isExtra ? 'd-none' : ''"
        >
          <questions-panel
            :question="questions[0]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(1)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="2" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[1]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(2)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 1" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="3" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[2]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(3)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 2" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="4" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[3]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(4)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 3" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="5" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[4]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(5)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 4" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="6" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[5]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(6)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 5" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="7" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[6]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(7)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 6" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="8" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[7]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(8)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 7" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="9" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[8]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(9)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 8" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="10" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[9]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(10)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 9" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="11" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[10]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(11)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 10" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="12" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[11]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(12)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 11" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="13" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[12]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(13)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 12" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="14" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[13]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="blue" @click="ClickContinue(14)" class="mr-4">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 13" class="mr-4">
                Volver
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="15" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[14]"
            :is-answer-marked0="isAnswerMarked0"
            :is-answer-marked1="isAnswerMarked1"
            :is-answer-marked2="isAnswerMarked2"
            :is-answer-marked3="isAnswerMarked3"
            :isCorrectAnswerMarked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel v-on:AnswerChange="AnswerChange" />
            <v-col align="center">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="mr-4"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
              <v-btn color="red" @click="e1 = 14" class="mr-4">
                Volver
              </v-btn>
              <v-btn color="indigo" @click="End()" class="mr-4">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange"
              :is-wildcard-used0="isWildcardUsed0"
              :is-wildcard-used1="isWildcardUsed1"
              :is-wildcard-used2="isWildcardUsed2"
              :is-wildcard-used3="isWildcardUsed3"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="16" style="background-color:rgba(0, 0, 0, 0)">
          <v-card
            height="180px"
            style="background-color:rgba(0, 0, 0, 0);
                   box-shadow: 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0), 0 0 0 0 rgba(0, 0, 0, 0);
align-items: center;"
          >
            <v-row align="center" justify="center">
              <v-col align="center">
                <v-img
                  src="../assets/piedra.png"
                  style="width: 780px; font-size: 48px; color: rgba(25, 25, 25, 100); align-items: center;"
                >
                  <div style="margin-top: -24px">
                    Aciertos totales: {{ totalCorrect }} <br />
                    Ronda alcanzada: {{ totalRanking + 1 }}
                  </div>
                </v-img>
              </v-col>
            </v-row>
          </v-card>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <v-col align="center">
              <v-btn color="red" @click="e1 = 15" class="mr-4">
                Volver
              </v-btn>
            </v-col>
          </v-row>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </v-container>
</template>

<script>
import Vue from "vue";
import json from "@/assets/questions.json";
import WildcardPanel from "@/components/WildcardPanel.vue";
import WildcardButtonPanel from "@/components/WildcardButtonPanel";
import QuestionsPanel from "@/components/QuestionsPanel";
import AnswerButtonPanel from "@/components/AnswerButtonPanel";

export default {
  name: "Questions",
  components: {
    AnswerButtonPanel,
    QuestionsPanel,
    WildcardButtonPanel,
    WildcardPanel
  },
  data() {
    return {
      e1: 1,
      isExtra: false,
      maxQuestions: 15,
      questions: json.questions,
      extras: json.extras,
      extraUsed: -1,
      isCategoryUsed0: false,
      isCategoryUsed1: false,
      isCategoryUsed2: false,
      isCategoryUsed3: false,
      isWildcardUsed0: false,
      isWildcardUsed1: false,
      isWildcardUsed2: false,
      isWildcardUsed3: false,
      isAnswerMarked0: false,
      isAnswerMarked1: false,
      isAnswerMarked2: false,
      isAnswerMarked3: false,
      isCorrectAnswerMarked: false,
      answers: [],
      totalCorrect: 0,
      totalRanking: 0,
      allWildcards: false
    };
  },
  created() {
    for (let i = 0; i < this.maxQuestions; i += 1) {
      this.answers.push(true);
    }
  },
  methods: {
    WildcardUsedChange(index) {
      switch (index) {
        case 0:
          this.isWildcardUsed0 = !this.isWildcardUsed0;
          if (this.isWildcardUsed0) this.extra(this.e1 - 1);
          break;
        case 1:
          this.isWildcardUsed1 = !this.isWildcardUsed1;
          if (this.isWildcardUsed1) this.fiftyPercent(this.e1 - 1);
          break;
        case 2:
          this.isWildcardUsed2 = !this.isWildcardUsed2;
          break;
        case 3:
          this.isWildcardUsed3 = !this.isWildcardUsed3;
          break;
      }
    },
    AnswerChange(index, newValue) {
      switch (index) {
        case 0:
          this.isAnswerMarked0 = newValue;
          break;
        case 1:
          this.isAnswerMarked1 = newValue;
          break;
        case 2:
          this.isAnswerMarked2 = newValue;
          break;
        case 3:
          this.isAnswerMarked3 = newValue;
          break;
      }
    },
    ClickContinue(index) {
      this.e1 = index + 1;
      if (this.e1 > 4) {
        this.allWildcards = true;
      }

      switch (this.questions[index - 1].correct) {
        case 0:
          this.answers[index - 1] = this.isAnswerMarked0;
          break;
        case 1:
          this.answers[index - 1] = this.isAnswerMarked1;
          break;
        case 2:
          this.answers[index - 1] = this.isAnswerMarked2;
          break;
        case 3:
          this.answers[index - 1] = this.isAnswerMarked3;
          break;
      }
      this.isCorrectAnswerMarked = false;
      this.isAnswerMarked0 = false;
      this.isAnswerMarked1 = false;
      this.isAnswerMarked2 = false;
      this.isAnswerMarked3 = false;
    },
    End() {
      this.e1 += 1;
      this.totalCorrect = 0;
      this.totalRanking = 0;
      switch (this.questions[this.maxQuestions - 1].correct) {
        case 0:
          this.answers[this.maxQuestions - 1] = this.isAnswerMarked0;
          break;
        case 1:
          this.answers[this.maxQuestions - 1] = this.isAnswerMarked1;
          break;
        case 2:
          this.answers[this.maxQuestions - 1] = this.isAnswerMarked2;
          break;
        case 3:
          this.answers[this.maxQuestions - 1] = this.isAnswerMarked3;
          break;
      }
      let f = true;
      for (let i = 0; i < this.maxQuestions; i += 1) {
        if (this.answers[i]) {
          this.totalCorrect += 1;
          if (f) {
            this.totalRanking += 1;
          }
        } else {
          f = false;
        }
      }
    },
    extra(questionIndex) {
      let ri = Math.floor(Math.random() * 2);
      if (this.extraUsed === -1) {
        Vue.set(this.questions, questionIndex, this.extras[ri]);
        this.extraUsed = ri;
      } else if (this.extraUsed === 0) {
        Vue.set(this.questions, questionIndex, this.extras[1]);
        this.extraUsed = 1;
      } else {
        Vue.set(this.questions, questionIndex, this.extras[0]);
        this.extraUsed = 0;
      }
    },
    fiftyPercent(questionIndex) {
      let i = 0;
      let newAnswers = [...this.questions[questionIndex].answers];
      do {
        let ri = Math.floor(Math.random() * 4);
        if (
          ri !== this.questions[questionIndex].correct &&
          newAnswers[ri] !== ""
        ) {
          i++;
          newAnswers[ri] = "";
        }
      } while (i < 2);
      Vue.set(this.questions[questionIndex], "answers", [...newAnswers]);
    }
  }
};
</script>

<style></style>
