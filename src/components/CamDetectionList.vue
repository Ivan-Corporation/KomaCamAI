<template>
  <div>
    <v-list>
      <v-list-subheader>Objects list:</v-list-subheader>

      <v-list-item
        v-for="(item, i) in items"
        :key="i"
        :value="item"
        color="info"
        rounded="shaped"
      >
        <template v-slot:prepend>
          <v-icon :icon="item.icon"></v-icon>
        </template>

        <v-list-item-title v-text="item.text"></v-list-item-title>
      </v-list-item>
    </v-list>
  </div>
</template>
<script setup>
import { ref } from "vue";

const items = ref([
  { text: "Bicycle", icon: "mdi-bicycle" },
  { text: "Person", icon: "mdi-account" },
  { text: "Car", icon: "mdi-car" },
  { text: "Motorcycle", icon: "mdi-motorbike" },
  { text: "Airplane", icon: "mdi-airplane" },
  { text: "Bus", icon: "mdi-bus" },
  { text: "Train", icon: "mdi-train" },
  { text: "Truck", icon: "mdi-truck" },
  { text: "Boat", icon: "mdi-sail-boat" },
  { text: "Traffic light", icon: "mdi-traffic-light" },
  { text: "Bird", icon: "mdi-bird" },
  { text: "Cat", icon: "mdi-cat" },
  { text: "Dog", icon: "mdi-dog" },
  { text: "Horse", icon: "mdi-horse" },
  { text: "Sheep", icon: "mdi-sheep" },
  { text: "Cow", icon: "mdi-cow" },
  { text: "Backpack", icon: "mdi-bag-personal" },
  { text: "Umbrella", icon: "mdi-umbrella" },
  { text: "Tie", icon: "mdi-tie" },
  { text: "Baseball bat", icon: "mdi-baseball-bat" },
  { text: "Bottle", icon: "mdi-bottle-soda" },
  { text: "Cup", icon: "mdi-cup" },
  { text: "Fork", icon: "mdi-silverware-fork" },
  { text: "Knife", icon: "mdi-knife" },
  { text: "Spoon", icon: "mdi-silverware-spoon" },
  { text: "Bowl", icon: "mdi-bowl" },
  { text: "Banana", icon: "mdi-peanut-outline" },
  { text: "Donut", icon: "mdi-chart-donut" },
  { text: "Apple", icon: "mdi-apple" },
  { text: "Chair", icon: "mdi-seat" },
  { text: "Couch", icon: "mdi-sofa-single" },
  { text: "Bed", icon: "mdi-bed" },
  { text: "Dining table", icon: "mdi-silverware" },
  { text: "TV", icon: "mdi-television" },
  { text: "Mouse", icon: "mdi-mouse" },
  { text: "Remote", icon: "mdi-remote" },
  { text: "Keyboard", icon: "mdi-keyboard" },
  { text: "Refrigerator", icon: "mdi-fridge" },
  { text: "Clock", icon: "mdi-clock" },
  { text: "Vase", icon: "mdi-flower-tulip" },
  { text: "Scissors", icon: "mdi-content-cut" },
  { text: "Teddy bear", icon: "mdi-teddy-bear" },
  { text: "Toothbrush", icon: "mdi-toothbrush" },
]);
</script>
<style></style>
