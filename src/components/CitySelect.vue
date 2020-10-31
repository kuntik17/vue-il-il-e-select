<template>
  <v-card class="mx-auto ma-12 pa-10" elevation="2" width="600px">
    <v-select
      :items="CitySelect"
      v-model="selectedCity"
      label="Alıcı İl"
      @change="citySelected()"
    ></v-select>
    <v-select
      :items="StateSelect"
      v-model="selectedState"
      label="Alıcı İlçe"
      @change="stateSelected()"
    ></v-select>
    <v-btn color="primary" @click="printCity">
      Devam
    </v-btn>
  </v-card>
</template>

<script>
import CityCodes from "../assets/CityCodes.json";

export default {
  data: () => ({
    CitySelect: [],
    StateSelect: [],
    DeliveryDistrict: null, // İlçe Kodu
    DeliveryCity: null, // İl Kodu
    selectedCity: null,
    selectedState: null,
    selectedPackage: null,
    cityList: CityCodes.CitySelect,
    stateList: [],
  }),
  methods: {
    packageSelected() {
      this.PackageType = this.packageItems.findIndex(
        (element) => element === this.selectedPackage
      );
      console.log(this.PackageType);
    },
    citySelected() {
      this.stateList = this.cityList.filter(
        (element) => element.City === this.selectedCity
      );

      this.stateList.forEach((element) => {
        this.StateSelect.push(element.State);
      });
    },
    stateSelected() {
      this.stateList = this.cityList.filter(
        (element) => element.State === this.selectedState
      );
      this.DeliveryCity = this.stateList[0].CityCode;
      this.DeliveryDistrict = this.stateList[0].StateCode;
    },
    printCity() {
      console.log(
        this.selectedCity, // Seçilen şehir
        this.DeliveryCity, // Seçilen şehir plaka numarası
        this.DeliveryDistrict, // Seçilen İlçe kodu
        this.selectedState // Seçilen ilçe
      );
    },
  },
  created() {
    var cities = [];
    this.cityList.forEach((element) => {
      cities.push(element.City);
    });
    var unique = cities.filter((v, i, a) => a.indexOf(v) === i);
    this.CitySelect = unique;
  },
};
</script>
