<template>
  <v-col class="mt-n2" align="center">
    <v-row>
      <v-btn
        fab
        dark
        :color="isWildcardUsed0 ? 'light-gray' : getColor()"
        @click="click(0)"
        class="mr-4"
      >
        <v-icon dark>
          mdi-numeric-1-circle
        </v-icon>
      </v-btn>
      <v-btn
        fab
        dark
        :color="isWildcardUsed1 ? 'light-gray' : getColor()"
        @click="click(1)"
        class="mr-4"
      >
        <v-icon dark>
          mdi-numeric-2-circle
        </v-icon>
      </v-btn>
      <v-btn
        fab
        dark
        :color="isWildcardUsed2 ? 'light-gray' : getColor()"
        @click="click(2)"
        class="mr-4"
      >
        <v-icon dark>
          mdi-numeric-3-circle
        </v-icon>
      </v-btn>
    </v-row>
  </v-col>
</template>

<script>
export default {
  name: "WildcardButtonPanel",
  props: {
    isWildcardUsed0: {
      type: Boolean,
      required: true
    },
    isWildcardUsed1: {
      type: Boolean,
      required: true
    },
    isWildcardUsed2: {
      type: Boolean,
      required: true
    },
    buttonColor: {
      type: String,
      required: true
    }
  },
  data() {
    return {};
  },
  methods: {
    click(index) {
      switch (index) {
        case 0:
          // this.isWildcardUsed0 = !this.isWildcardUsed0;
          this.$emit("WildcardUsedChange", index);
          break;
        case 1:
          // this.isWildcardUsed1 = !this.isWildcardUsed1;
          this.$emit("WildcardUsedChange", index);
          break;
        case 2:
          // this.isWildcardUsed2 = !this.isWildcardUsed2;
          this.$emit("WildcardUsedChange", index);
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
