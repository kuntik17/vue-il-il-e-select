<template>
  <v-app>
    <v-app-bar app color="primary" dark> </v-app-bar>

    <v-main>
      <CitySelect />
    </v-main>
  </v-app>
</template>

<script>
import CitySelect from "./components/CitySelect";

export default {
  name: "App",

  components: {
    CitySelect,
  },

  data: () => ({
    //
  }),
};
</script>
