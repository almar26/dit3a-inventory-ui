<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="3" md="3">
        <DashboardCard
          :title="`Total Products`"
          :value="25"
          :color="`green`"
          :icon="`mdi-package-variant-closed`"
        />
      </v-col>
      <v-col cols="12" sm="3" md="3">
        <DashboardCard
          :title="`Low Stock Products`"
          :value="5"
          :color="`orange`"
          :icon="`mdi-package-variant-minus`"
        />
      </v-col>
      <v-col cols="12" sm="3" md="3">
        <DashboardCard
          :title="`Out of Stock Product`"
          :value="5"
          :color="`red`"
          :icon="`mdi-package-variant`"
        />
      </v-col>
      <v-col cols="12" sm="3" md="3">
        <DashboardCard
          :title="`Sold products`"
          :value="5"
          :color="`blue`"
          :icon="`mdi-package-variant-closed-plus`"
        />
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="4">
        <v-row class="mt-2">
          <v-col cols="12">
            <v-card class="mt-4 mx-auto" elevation="0">
              <v-sheet
                class="v-sheet--offset mx-auto"
                color="cyan"
                elevation="12"
                max-width="calc(100% - 32px)"
              >
                <v-sparkline
                  :labels="labels"
                  :value="value"
                  color="white"
                  line-width="2"
                  padding="16"
                ></v-sparkline>
              </v-sheet>
              <v-card-text class="pt-0">
                <div class="text-h6 font-weight-light mb-2">
                  Daily Collections
                </div>
                <div class="subheading font-weight-light grey--text">
                  Last Campaign Performance
                </div>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col cols="12">
            <v-card class="mt-4 mx-auto" elevation="0">
              <v-sheet
                class="v-sheet--offset mx-auto"
                color="warning"
                elevation="12"
                max-width="calc(100% - 32px)"
              >
                <v-sparkline
                  :labels="labels"
                  :value="value"
                  color="white"
                  line-width="2"
                  padding="16"
                ></v-sparkline>
              </v-sheet>

              <v-card-text class="pt-0">
                <div class="text-h6 font-weight-light mb-2">
                  Daily Collections
                </div>
                <div class="subheading font-weight-light grey--text">
                  Last Campaign Performance
                </div>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="12" md="8">
        <v-card elevation="0">
          <v-card-title>
            Nutrition
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            :headers="headers"
            :items="desserts"
            :items-per-page="5"
            :search="search"
            class="elevation-0"
          ></v-data-table>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import DashboardCard from "../components/DashboardCard.vue";
export default {
  data() {
    return {
      search: "",
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: 1,
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: 1,
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: 7,
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: 8,
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: 16,
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: 0,
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: 2,
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: 45,
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: 22,
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: 6,
        },
      ],
      labels: ["12am", "3am", "6am", "9am", "12pm", "3pm", "6pm", "9pm"],
      value: [200, 675, 410, 390, 310, 460, 250, 240],
    };
  },
};
</script>
<style scoped>
.v-sheet--offset {
  top: -24px;
  position: relative;
}
</style>