<template>
  <v-row>
    <v-col class="text-center" cols="12">
      <img
        src="/v.png"
        alt="Vuetify.js"
        class="mb-5"
      >
      <blockquote class="blockquote">
        &#8220;First, solve the problem. Then, write the code.&#8221;
        <footer>
          <small>
            <em>&mdash;John Johnson</em>
          </small>
        </footer>
      </blockquote>
    </v-col>
    <v-col cols="3">
      <cards-component :title="`Sample Card`" :value="100" :icon="`mdi-cog`" :color="`purple`"></cards-component>
    </v-col>
  </v-row>
</template>

<script>
import CardsComponent from '../components/CardsComponent.vue'
export default {
  components: { CardsComponent },
  name: 'InspirePage'
}
</script>
