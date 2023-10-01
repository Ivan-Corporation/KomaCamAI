<script setup>
import FaceLandmark from "./components/FaceLandmark.vue";
import CamDetection from "./components/CamDetection.vue";
import CamDetectionList from "./components/CamDetectionList.vue";
import { ref } from "vue";

const tab = ref("one");
</script>

<template>
  <v-card class="pa-md-4 mx-auto card_container">
    <v-tabs v-model="tab" bg-color="dark">
      <v-tab value="one">KomCam Detector</v-tab>
      <v-tab value="two">KomCam LandMark</v-tab>
      <v-tab value="three">KomCam List</v-tab>
    </v-tabs>

    <v-card-text>
      <v-window v-model="tab">
        <v-window-item value="one">
          <CamDetection @change-tab-three="tab = 'three'"/>
        </v-window-item>

        <v-window-item value="two">
          <FaceLandmark  />
        </v-window-item>

        <v-window-item value="three"> 
          <CamDetectionList/>
        </v-window-item>
      </v-window>
    </v-card-text>
  </v-card>
</template>

<style scoped>
.card_container {
  width: 850px;
  height: 850px;

}
@media (max-width: 950px) {
  .card_container {
    width: 100%;
  }
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
