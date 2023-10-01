<template>
  <v-list>
    <v-list-subheader>Objects list:</v-list-subheader>

    <v-list-item
      v-for="(item, i) in items"
      :key="i"
      :value="item"
      color="primary"
      rounded="shaped"
    >
      <template v-slot:prepend>
        <v-icon :icon="item.icon"></v-icon>
      </template>

      <v-list-item-title v-text="item.text"></v-list-item-title>
    </v-list-item>
  </v-list>
</template>
<script setup>
import {ref} from 'vue'

const items = ref([
  { text: "Real-Time", icon: "mdi-clock" },
  { text: "Audience", icon: "mdi-account" },
  { text: "Conversions", icon: "mdi-flag" },
]);
</script>
<style></style>
