<template>
  <div class="d-flex align-center justify-center"  style="height: 100vh;">
    <v-card width="500" class="py-8">
      <v-card-text>
        <h1 class="text-center">Login</h1>
        <v-form class="mx-5 mt-10">
          <v-text-field label="Email Address" prepend-inner-icon="mdi-email" outlined></v-text-field>
          <v-text-field label="Password" type="password" prepend-inner-icon="mdi-lock" outlined></v-text-field>
          <v-btn block color="primary">Sign In</v-btn>
          <v-btn block class="mt-2">Cancel</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
    // layout: "auth"
}
</script>