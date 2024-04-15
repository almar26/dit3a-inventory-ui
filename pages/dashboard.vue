<template>
  <v-container>
    <v-row>
      <v-col cols="3">
        <CardsComponent :title="`Active Students`" :value="25" :icon="`mdi-account`" :color="`pink`"/>
      </v-col>
      <v-col cols="3">
        <CardsComponent :title="`Inactive Students`" :value="13" :icon="`mdi-account`" :color="`blue`"/>
      </v-col>
      <v-col cols="3">
        <CardsComponent />
      </v-col>
      <v-col cols="3">
        <CardsComponent />
      </v-col>
      
    </v-row>
  </v-container>
</template>
<script>
import CardsComponent from "../components/CardsComponent.vue"
export default {
  data() {
    return {};
  },
};
</script>
<style scoped>
.v-sheet--offset {
  top: -24px;
  position: relative;
}
</style>