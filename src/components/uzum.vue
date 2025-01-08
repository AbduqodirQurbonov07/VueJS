<template>
  <div class="flex gap-4 m-6">
    <div v-for="uz in uzum" :key="uz.mal" class="hover:shadow-md w-64 h-78">
      <div class="overflow-hidden">
        <img
          class="h-78 w-64 rounded-xl hover:scale-105 hover:transition duration-700"
          :src="getImg(uz?.img)"
          alt="shashb"
        />
      </div>
      <div class="py-2 px-3">
        <p class="max-w-52">
          {{ uz.mal }}
        </p>
        <ul class="flex items-center">
          <li><img src="../images/star.svg" alt="" /></li>
          <li class="text-slate-500 text-xs">{{ uz.sharh }}</li>
        </ul>
        <p class="inline bg-yellow-300 text-sm">{{ uz.oyiga }}</p>
      </div>
      <div class="px-3 py-4 flex flex-row">
        <ul>
          <li class="text-sm line-through text-slate-500">{{ uz.narx }}</li>
          <li class="">{{ uz.chegirma }}</li>
        </ul>
        <img class="relative left-24" src="../images/basket.svg" alt="" />
      </div>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref, computed } from "vue";
function getImg(path) {
  return new URL(path, import.meta.url).href;
}

let uzum = [
  {
    mal: "Ofis texnikalari uchun qog'oz varaqlari Sylvamo Svetotopy, A4f C07/3, 500 varaq",
    sharh: "4.9(21739 sharhlar)",
    oyiga: "2 975 so'm/oyiga",
    narx: "55 000",
    chegirma: "42000so'm",
    img: "../images/qogoz.jpg",
  },
  {
    mal: "Changyutgich Bosch BGC21X300",
    sharh: "4.7(256 sharhlar)",
    oyiga: "212 570 so'm/oyiga",
    narx: " 3 900 260",
    chegirma: "3 001 000so'm",
    img: "../images/changyutkich.jpg",
  },
  {
    mal: "Televizor Artel A43KF5500 SMART TV Android, qora",
    sharh: "4.9(236 sharhlar)",
    oyiga: "186 220 so'm/oyiga",
    narx: "4 999 000",
    chegirma: "2 629 000so'm",
    img: "../images/tv.jpg",
  },
  {
    mal: "Ikki kamerali Biryusa sovutgich, BIRYUSA-124 modeli, hajmi 205 litr",
    sharh: "4.9(27 sharhlar)",
    oyiga: "177 012 so'm/oyiga",
    narx: "4 580 000",
    chegirma: "2 499 000so'm",
    img: "../images/muzlatkich.jpg",
  },
  {
    mal: "Oqartiruvchi Vanish Oxi Advance, 400 ml",
    sharh: "4.8(10 sharhlar)",
    oyiga: "4 213 so'm/oyiga",
    narx: "70 000",
    chegirma: "59 490so'm",
    img: "../images/vanish.jpg",
  },
];
</script>
<style>
/* @import url(https://fonts.googleapis.com/css2?family=Kanit:wght@100;200;300;400;500;600;800;900&display=swap); */

/* * { */
/* font-family: "Kanit", sans-serif; */
/* } */
</style>
