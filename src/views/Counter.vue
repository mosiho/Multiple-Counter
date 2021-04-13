<template>
  <div class="pa-6">
    <v-container class="white rounded-xl pa-10 pt-2">
    <!-- Input form -->
      <v-text-field
        type="number"
        v-model="newstepnum"
        @click:append="addstep"
        @keyup.enter="addstep"
        outlined
        label="Enter a number"
        append-icon="mdi-plus"
        class="mx-3 mt-5"
        hint="This only accept numbers like 4, -2, 4.3 or -1.3"
        :rules="inputrules"
      >
      </v-text-field>
      <v-row no-gutters>
        <!-- Creating cards based on grid system -->
        <v-col
          v-for="step in steps"
          :key="step.number"
          cols="12"
          md="4"
          class="pa-4"
        >
          <v-card
            class="pa-2 d-flex align-content-center flex-wra pr-5"
            outlined
            tile
          >
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title class="mb-1">
                  Step {{ step.number }}
                </v-list-item-title>
              </v-list-item-content>

             <!-- Display calculated number -->
              <v-list-item-avatar
                tile
                color="grey lighten-4"
                class="rounded-l-xl"
              >
                {{ step.sumnum }}
              </v-list-item-avatar>
            </v-list-item>

            <v-card-actions>
              <div class="text-center">
                <v-btn
                  class="rounded-r-xl"
                  color="primary"
                  dark
                  @click="editstep(step.id)"
                >
                  Run
                </v-btn>
              </div>
            </v-card-actions>
            <v-list-item-action>
              <v-btn icon @click.stop="deletestep(step.id)">
                <v-icon color="red lighten-2">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newstepnum: "",
      steps: [],
      //Input conditions
      inputrules: [
        (v) => (v >= -99 && v <= 99) || "Number has to be between -99 and 99",
      ],
    };
  },
  methods: {
    addstep() {
      let newstep = {
        //I use "id" to control duplicate numbers
        id: Date.now(),
        number: Number(this.newstepnum),
        sumnum: 0,
        newvalue: 0,
      };
      if (
        this.newstepnum != "" &&
        this.newstepnum <= 99 &&
        this.newstepnum >= -99
      ) {
        this.steps.push(newstep);
        this.newstepnum = "";
      }
    },
      // Add numbers for each step
    editstep(id) {
      for (var i in this.steps) {
        if (this.steps[i].id == id) {
          this.steps[i].newvalue = this.steps[i].newvalue + 1;
          this.steps[i].sumnum = this.steps[i].number * this.steps[i].newvalue;
        }
      }
    },
      // Delete the selected card
    deletestep(id) {
      this.steps = this.steps.filter((step) => step.id !== id);
    },
  },
};
</script>
