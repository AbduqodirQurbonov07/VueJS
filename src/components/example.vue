<template>
  <div
    class="h-screen w-screen flex flex-col items-center justify-center gap-5"
  >
    <div
      :class="[isError ? 'flex' : 'hidden']"
      class="flex flex-col items-start w-[395px] p-2 border-red-500 border rounded-xl gap-2"
    >
      <p class="text-red-500 font-semibold text-lg">Xatolik</p>
      <p class="text-red-600">Login yoki parol xato</p>
    </div>

    <div
      :class="[isLogged && !isError ? 'flex' : 'hidden']"
      class="flex flex-col items-start w-[395px] p-2 border-green-500 border rounded-xl gap-2"
    >
      <p class="text-green-600">Ro'yxatdan o'tdingiz</p>
    </div>

    <form action="" class="flex flex-col gap-3 border p-10 rounded-lg">
      <p class="flex flex-col items-center justify-center text-black text-2xl">
        Xush kelibsiz!
      </p>
      <p class="flex flex-col text-slate-500 items-center">
        iltimos hisob malumotlarini kiriting
      </p>
      <p>Login</p>
      <input
        v-model="login"
        class="px-4 py-1.5 border border-slate-200 rounded-lg w-80"
        type="text"
        placeholder="Enter you login..."
      />
      <p>Parol</p>
      <input
        v-model="parol"
        class="px-4 py-1.5 border border-slate-200 rounded-lg w-8`cbh 0"
        type="password"
        placeholder="Enter you password..."
      />
      <ul class="flex gap-2">
        <input class="flex" type="checkbox" />
        <label for="">eslab qolish</label>
      </ul>
      <button
        v-if="!isLoading"
        @click="submitForm"
        class="bg-indigo-600 rounded-lg text-slate-100 px-[130px] text-lg py-1"
      >
        kirish
      </button>
      <button
        v-else
        @click="submitForm"
        class="bg-indigo-600 rounded-lg text-slate-100 px-[130px] text-lg py-1"
      >
        Loading...
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
let isLogged = ref(false);
let login = ref("");
let isLoading = ref(false);
let isError = ref(false);
let parol = ref("");
let users = reactive([
  { parol: "1234567", login: "Abubakr" },
  { parol: "12345", login: "Abduqodir" },
  { parol: "123", login: "Muhammadrajab" },
]);
function submitForm() {
  isLoading.value = true;
  setTimeout(() => {
    const user = users.find(
      (user) => user.login === login.value && user.parol === parol.value
    );
    if (user) {
      isLogged.value = true;
      isError.value = false;
    } else {
      isLogged.value = false;
      isError.value = true;
    }

    isLoading.value = false;
    login.value = "";
    parol.value = "";
    setTimeout(() => {
      isLogged.value = false;
      isError.value = false;
    }, 5000);
  }, 3000);
}
</script>

<style scoped>
@import url(https://fonts.googleapis.com/css2?family=Kanit:wght@100;200;300;400;500;600;800;900&display=swap);

body {
  font-family: "Kanit", sans-serif;
}
</style>
