<template>
  <div>
    <p>{{ sanoq }}</p>
    <button @click="add">Oshirish</button>
    <button id="minus" @click="minus">kamaytirish</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
let sanoq = ref(0);
function add() {
  sanoq.value++;
}
function minus() {
  sanoq.value--;
}
</script>

<style scoped>
button {
  color: white;
  background-color: darkgreen;
  padding: 10px 33px;
  border-radius: 8px;
  border: 1px solid transparent;
}
#minus {
  color: white;
  background-color: darkred;
  padding: 10px 33px;
  border-radius: 8px;
  border: 1px solid transparent;
}
</style>
