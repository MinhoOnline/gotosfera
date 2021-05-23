<template>
  <v-container fluid>
    <!--    <v-btn class="ma-2" color="secondary" @click="expand = !expand">-->
    <!--      Expand X Transition-->
    <!--    </v-btn>-->
    <!--    <v-expand-x-transition>-->
    <!--      <v-card-->
    <!--        v-show="expand"-->
    <!--        height="100"-->
    <!--        width="100"-->
    <!--        class="mx-auto secondary"-->
    <!--      ></v-card>-->
    <!--    </v-expand-x-transition>-->
    <v-overlay absolute="false" :value="end" opacity="0.8">
      <v-row align="center" justify="center" style="margin-top: 370px">
        <v-col align="center">
          <v-img
            v-if="totalCorrectP2 < totalCorrectP1"
            src="../assets/winnerP1.png"
            style="width: 320px; color: rgba(25, 25, 25, 100); align-items: center; z-index: 1000"
          >
          </v-img>
          <v-img
            v-if="totalCorrectP2 > totalCorrectP1"
            src="../assets/winnerP2.png"
            style="width: 320px; color: rgba(25, 25, 25, 100); align-items: center; z-index: 1000"
          >
          </v-img>
          <v-img
            class="mt-n14"
            src="../assets/piedra.png"
            style="width: 750px; font-size: 48px; color: rgba(25, 25, 25, 100); align-items: center;"
          >
            <div style="margin-top: -24px">
              Aciertos Feelink: {{ totalCorrectP1 }} <br />
              Aciertos Enterra: {{ totalCorrectP2 }}
            </div>
          </v-img>
        </v-col>
      </v-row>
      <v-row align="center" justify="center" style="margin-top: 60px">
        <v-btn color="red" @click="end = false">
          Close
        </v-btn>
      </v-row>
    </v-overlay>
    <v-row style="margin-top: 470px;background-color: rgba(0, 0, 0, 0.6)">
      <v-col>
        <wildcard-panel
          :is-wildcard-used0="isP1WildcardUsed0"
          :is-wildcard-used1="isP1WildcardUsed1"
          :is-wildcard-used2="isP1WildcardUsed2"
        />
      </v-col>
      <v-col>
        <wildcard-panel
          :is-wildcard-used0="isP2WildcardUsed0"
          :is-wildcard-used1="isP2WildcardUsed1"
          :is-wildcard-used2="isP2WildcardUsed2"
        />
      </v-col>
    </v-row>
    <v-stepper
      class="mx-0 px-0"
      alt-labels
      v-model="e1"
      style="background-color:rgba(0, 0, 0, 0)"
    >
      <v-stepper-header
        class="mb-n14 mt-n12 mx-2 px-0 pt-8"
        style="box-shadow: 0px 0px 0px 0px rgba(0, 0, 0, 0), 0px 0px 0px 0px rgba(0, 0, 0, 0), 0px 0px 0px 0px rgba(0, 0, 0, 0);
              background-color: rgba(0, 0, 0, 0.6)"
      >
        <v-row v-for="i in 10" :key="i">
          <v-stepper-step
            :complete="e1 > i"
            :step="i"
            color="red darken-1"
            :rules="[() => answersP1[i - 1]]"
          >
          </v-stepper-step>
        </v-row>
        <v-row>
          <v-divider vertical></v-divider>
        </v-row>
        <v-row v-for="i in 10" :key="i">
          <v-stepper-step
            :complete="e2 > i"
            :step="i"
            color="yellow darken-2"
            :rules="[() => answersP2[i - 1]]"
          >
          </v-stepper-step>
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
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="ml-10 mr-16">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
                class="ml-n8 mr-4"
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
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="2" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[1]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(2)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 1;
                  e2 = 1;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="3" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[2]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(3)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 2;
                  e2 = 2;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="4" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[3]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(4)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 3;
                  e2 = 3;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="5" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[4]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(5)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 4;
                  e2 = 4;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="6" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[5]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(6)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 5;
                  e2 = 5;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="7" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[6]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(7)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 6;
                  e2 = 6;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="8" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[7]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(8)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 7;
                  e2 = 7;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="9" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[8]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(9)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 8;
                  e2 = 8;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="10" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[9]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(10)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 9;
                  e2 = 9;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="11" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[10]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(11)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 10;
                  e2 = 10;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="12" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[11]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(12)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 11;
                  e2 = 11;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="13" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[12]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(13)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 12;
                  e2 = 12;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="14" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[13]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn color="blue" @click="ClickContinue(14)">
                Continuar
                <v-icon right> mdi-arrow-right-circle </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 13;
                  e2 = 13;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
            />
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="15" style="background-color:rgba(0, 0, 0, 0)">
          <questions-panel
            :question="questions[14]"
            :is-p1-answer-marked0="isP1AnswerMarked0"
            :is-p1-answer-marked1="isP1AnswerMarked1"
            :is-p1-answer-marked2="isP1AnswerMarked2"
            :is-p1-answer-marked3="isP1AnswerMarked3"
            :is-p2-answer-marked0="isP2AnswerMarked0"
            :is-p2-answer-marked1="isP2AnswerMarked1"
            :is-p2-answer-marked2="isP2AnswerMarked2"
            :is-p2-answer-marked3="isP2AnswerMarked3"
            :is-correct-answer-marked="isCorrectAnswerMarked"
          />
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-14"> </v-row>
          <v-row class="mt-16">
            <answer-button-panel
              v-on:AnswerChange="AnswerChange1"
              button-color="red"
            />
            <answer-button-panel
              v-on:AnswerChange="AnswerChange2"
              button-color="yellow"
            />
            <v-col align="center" class="mx-n16 px-n6">
              <v-btn
                color="green darken-2"
                @click="isCorrectAnswerMarked = !isCorrectAnswerMarked"
              >
                <v-icon dark>
                  mdi-check-bold
                </v-icon>
              </v-btn>
            </v-col>
            <v-col align="center" class="mx-n16">
              <v-btn
                color="red"
                @click="
                  e1 = 14;
                  e2 = 14;
                "
              >
                Volver
              </v-btn>
            </v-col>
            <v-col align="center" class="ml-n16">
              <v-btn color="indigo" @click="End()">
                Fin
                <v-icon right> mdi-medal </v-icon>
              </v-btn>
            </v-col>
            <wildcard-button-panel
              align="left"
              v-on:WildcardUsedChange="WildcardUsedChange1"
              :is-wildcard-used0="isP1WildcardUsed0"
              :is-wildcard-used1="isP1WildcardUsed1"
              :is-wildcard-used2="isP1WildcardUsed2"
              button-color="red"
            />
            <wildcard-button-panel
              v-on:WildcardUsedChange="WildcardUsedChange2"
              :is-wildcard-used0="isP2WildcardUsed0"
              :is-wildcard-used1="isP2WildcardUsed1"
              :is-wildcard-used2="isP2WildcardUsed2"
              button-color="yellow"
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
                    Aciertos Jugador Rojo: {{ totalCorrectP1 }} <br />
                    Aciertos Jugador Amarillo: {{ totalCorrectP2 }}
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
      e2: 1,
      isExtra: false,
      maxQuestions: 15,
      questions: json.questions,
      extras: json.extras,
      extraUsed: -1,
      isP1WildcardUsed0: false,
      isP1WildcardUsed1: false,
      isP1WildcardUsed2: false,
      isP2WildcardUsed0: false,
      isP2WildcardUsed1: false,
      isP2WildcardUsed2: false,
      isP1AnswerMarked0: false,
      isP1AnswerMarked1: false,
      isP1AnswerMarked2: false,
      isP1AnswerMarked3: false,
      isP2AnswerMarked0: false,
      isP2AnswerMarked1: false,
      isP2AnswerMarked2: false,
      isP2AnswerMarked3: false,
      isCorrectAnswerMarked: false,
      answersP1: [],
      answersP2: [],
      totalCorrectP1: 0,
      totalCorrectP2: 0,
      end: false,
      expand: false
    };
  },
  watch: {
    expand(val) {
      val &&
        setTimeout(() => {
          this.expand = !this.expand;
        }, 4000);
    }
  },
  created() {
    for (let i = 0; i < this.maxQuestions; i += 1) {
      this.answersP1.push(true);
      this.answersP2.push(true);
    }
  },
  methods: {
    WildcardUsedChange1(index) {
      switch (index) {
        case 0:
          this.isP1WildcardUsed0 = !this.isP1WildcardUsed0;
          if (this.isP1WildcardUsed0) this.extra(this.e1 - 1);
          break;
        case 1:
          this.isP1WildcardUsed1 = !this.isP1WildcardUsed1;
          break;
        case 2:
          this.isP1WildcardUsed2 = !this.isP1WildcardUsed2;
          break;
      }
    },
    WildcardUsedChange2(index) {
      switch (index) {
        case 0:
          this.isP2WildcardUsed0 = !this.isP2WildcardUsed0;
          if (this.isP2WildcardUsed0) this.extra(this.e1 - 1);
          break;
        case 1:
          this.isP2WildcardUsed1 = !this.isP2WildcardUsed1;
          break;
        case 2:
          this.isP2WildcardUsed2 = !this.isP2WildcardUsed2;
          break;
      }
    },
    AnswerChange1(index, newValue) {
      switch (index) {
        case 0:
          this.isP1AnswerMarked0 = newValue;
          break;
        case 1:
          this.isP1AnswerMarked1 = newValue;
          break;
        case 2:
          this.isP1AnswerMarked2 = newValue;
          break;
        case 3:
          this.isP1AnswerMarked3 = newValue;
          break;
      }
    },
    AnswerChange2(index, newValue) {
      switch (index) {
        case 0:
          this.isP2AnswerMarked0 = newValue;
          break;
        case 1:
          this.isP2AnswerMarked1 = newValue;
          break;
        case 2:
          this.isP2AnswerMarked2 = newValue;
          break;
        case 3:
          this.isP2AnswerMarked3 = newValue;
          break;
      }
    },
    ClickContinue(index) {
      this.e1 = index + 1;
      this.e2 = index + 1;

      switch (this.questions[index - 1].correct) {
        case 0:
          this.answersP1[index - 1] = this.isP1AnswerMarked0;
          break;
        case 1:
          this.answersP1[index - 1] = this.isP1AnswerMarked1;
          break;
        case 2:
          this.answersP1[index - 1] = this.isP1AnswerMarked2;
          break;
        case 3:
          this.answersP1[index - 1] = this.isP1AnswerMarked3;
          break;
      }

      switch (this.questions[index - 1].correct) {
        case 0:
          this.answersP2[index - 1] = this.isP2AnswerMarked0;
          break;
        case 1:
          this.answersP2[index - 1] = this.isP2AnswerMarked1;
          break;
        case 2:
          this.answersP2[index - 1] = this.isP2AnswerMarked2;
          break;
        case 3:
          this.answersP2[index - 1] = this.isP2AnswerMarked3;
          break;
      }

      this.isCorrectAnswerMarked = false;
      this.isP1AnswerMarked0 = false;
      this.isP1AnswerMarked1 = false;
      this.isP1AnswerMarked2 = false;
      this.isP1AnswerMarked3 = false;
      this.isP2AnswerMarked0 = false;
      this.isP2AnswerMarked1 = false;
      this.isP2AnswerMarked2 = false;
      this.isP2AnswerMarked3 = false;
    },
    End() {
      this.totalCorrectP1 = 0;
      this.totalCorrectP2 = 0;
      switch (this.questions[this.e1 - 1].correct) {
        case 0:
          this.answersP1[this.e1 - 1] = this.isP1AnswerMarked0;
          break;
        case 1:
          this.answersP1[this.e1 - 1] = this.isP1AnswerMarked1;
          break;
        case 2:
          this.answersP1[this.e1 - 1] = this.isP1AnswerMarked2;
          break;
        case 3:
          this.answersP1[this.e1 - 1] = this.isP1AnswerMarked3;
          break;
      }
      switch (this.questions[this.e1 - 1].correct) {
        case 0:
          this.answersP2[this.e1 - 1] = this.isP2AnswerMarked0;
          break;
        case 1:
          this.answersP2[this.e1 - 1] = this.isP2AnswerMarked1;
          break;
        case 2:
          this.answersP2[this.e1 - 1] = this.isP2AnswerMarked2;
          break;
        case 3:
          this.answersP2[this.e1 - 1] = this.isP2AnswerMarked3;
          break;
      }

      for (let i = 0; i < this.e1; i += 1) {
        if (this.answersP1[i]) {
          this.totalCorrectP1 += 1;
        }
        if (this.answersP2[i]) {
          this.totalCorrectP2 += 1;
        }
      }
      this.end = !this.end;
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

<style>
.v-stepper__step__step {
  font-size: 1.2rem !important;
}
</style>
