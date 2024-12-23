<template>
  <div
    class="bg-black w-screen h-screen flex justify-center items-center flex-col gap-10"
  >
    <div class="flex items-center justify-center">
      <img
        v-if="isOn == true"
        class="w-150 h-50"
        src="../images/light-on.jpg"
        alt=""
      />
      <img
        v-else="isOff == false"
        class="w-100 h-80"
        src="../images/light-off.jpg"
        alt=""
      />
    </div>
    <div class="flex gap-6">
      <button
        @click="isOn"
        class="bg-slate-50 px-4 text-green-700 py-2 rounded-lg"
      >
        On
      </button>
      <button
        @click="isOff"
        class="bg-slate-50 py-2 text-red-700 px-4 rounded-lg"
      >
        Off
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

let isOn = ref(true);
let isOff = ref(false);
</script>
